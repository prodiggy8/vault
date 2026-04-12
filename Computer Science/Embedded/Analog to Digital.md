Analog -> continuous function of voltage

Need to convert to 0 and 1

==Fourier Transform: convert a signal from time domain to frequency domain==



==**Nyquist Theorem**==
==If a signal has max frequency $f_{max}$ and a sampling frequency of $f_s$ we can reconstruct the signal perfectly if==
==$$f_s > 2f_{max}$$==

==**Valvano Postulate**==
==Not a theorem, more like an observation: in embedded systems, we need $f_s > 10f_{max}$ to be safe.==

### A2C on the RP2040

Can be connected to 4 different pins
==12-bit resolution==
- one shot
- free running
- FIFO
- Interrupt when data is available
- Reads 3.3V
  
==ADC0, 1, 2 on GPIO26, 27, 28==
4th ADC is for battery, reading half of Vsys (5v)

Since we have 12 bits we have linear interpolation:
(max range) / 4096 = delta per bit

**How to use?**
1. ==Pull out of reset==
	==`set_bits(RESETS_BASE, 1 << 0)`==
	==`clear_bits(RESETS_BASE, 1 << 0)`==
	
2. ==Disable digital input and output on the pad==
	==`write_reg(PADS_BANK0_BASE + (pin + 1) * 4, 1 << 7)`==
	==**Output disable**==
	
3. ==Enable ADC in CS register==
	==`write_reg(ADC_BASE + ACS_CS, 0x1)` **enabling**==
	
4. ==Select pin to use in AINSEL in CS==
5. ==Start conversion in CS==
	==`write_reg(ADC_BASE + ADC_CS`==
		==`0x1 |`==     
		==`(1 << 11 << (26 - pin) |`  sets **ADC pin** (0-2)==
		==`(1 << (2 + mode))` sets **mode** (read once, many, FIFO)==
6. ==Wait until ready==
	==`read_reg(ADC_BASE + ADC_CS) & (1 << 8) != 0`==
7. ==Read the 12 bit result==
	==`read_reg(ADC_BASE + ADC_RESULT) & 0xFFF`==

Both **read many and once** work the same way as presented above

==We can set a DIV register to adjust sampling rate of CS_START_MANY==
==`write_reg(ADC_BASE + 0x10, DIVISOR)`==

==cycles = 1 + INTDIV + FRACDIV / 256==

==Sampling rate is by standard every 96 clock cycles, clock is 48MHz.==
==$\frac{48MHz}{96}=500kHz$ or 1 new sample every $2 {\mu}s$==

==Setting DIV.INT to 47999 will run the ADC at 1ksps, if running from a 48MHz clock.==

**FIFO**

We need to setting up start many we can use FIFO to read instead of result

1. ==Enable FIFO in FCS==
==`write_reg(ADC_BASE + FCS, 1 << 0)`==
2. ==Can be read with interrupts or status in FCS==
==Status example:==
	
3. ==If FIFO is full, FCS OVER is set, anything after is lost==
==`read_reg(ADC_BASE + FCS) & (1 << 8)` EMPTY==
==`read_reg(ADC_BASE + FCS) & (1 << 9)` FULL==
==`read_reg(ADC_BASE + FCS) & (1 << 11)` OVER==
==`read_reg(ADC_BASE + FCS) & (0b1111 << 16)` LEVEL (0 - 8 inclusive)==

4. ==Read results==
==`read_reg(ADC_BASE + FIFO) & 0xFFF`==

**Interrupts for the FIFO**

1. ==Set the FCS.THRESH = n==
	==`write_reg(ADC_BASE + FCS, n << 24)`, $n \leq 8$==
2. ==Follow normal interrupt process using==
	==`ADC_BASE + INTR` (bit 0: interrupt available?)==
	==`ADC_BASE + INTE` (bit 0: interrupt enable)==
	==`ADC_BASE + INTS` (bit 0: interrupt available)==

==Other:==
==FCS.SHIFT -> right shifts 12-bit ADC to 8 bits, useful when little precision is needed/working with bytes==
==FCS.ERR -> error flag==


#### ==SAR==
- ==Generates voltage and compares to input==
- ==Binary search fashion==
- ==Example: 1.5V==

| **Step** | **Guess** | Volts    | Result |
| -------- | --------- | -------- | ------ |
| 1        | 1000      | 1.65V    | >      |
| 2        | 0100      | 0.825V   | <      |
| 3        | 0110      | 1.2375V  | <      |
| 4        | 0111      | 1.44375V | <      |
==Answer: 0111==


==**Exam 2 Stuff**==
==Calculate bit number==

==$Sensitivity = \frac{\Delta V}{\Delta{cm}}=xV/cm$==
==$\Delta{V}_{req}=Sensitivity \cdot Precision$==
==Now find $n$:==
==$\frac{V_{max}}{2^n} > \Delta{V}_{req}$==

==Finding bits given voltage: $\frac{input}{V_{max}}*4095$==

