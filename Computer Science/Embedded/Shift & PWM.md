
`fn send_all(bits: u32) {`
	`for i in 0..16 {`
		`send((bits >> i) & 0x1);`
	`}`
	`write_reg(SIO_BASE + 0x18, 1 << STCP_PIN);`
	`write_reg(SIO_BASE + 0x14, 1 << STCP_PIN);`
`}`

`fn send(bit: u32) {`
	`let offset: u32 = if bit == 1 { 0x14 } else { 0x18 }`

	write_reg(SIO_BASE + 0x18, 1 << SHCP_PIN);
	write_reg(SIO_BASE + offset, 1 << DS_PIN);
	write_reg(SIO_BASE + 0x14, 1 << SHCP_PIN);
`}`


**Pulse Width Modulation**

In HW2, we just delayed, but there is module for PWM.

**Period:** time for signal to repeat
**Duty Cycle**: percentage of time the signal is high

PWM module has running counter
Achieves a specific value and then goes back to 0
PWM output is high for a certain part of this time (defined by threshold)

![[Pasted image 20251108212434.png]]

Period set in TOP
Duty cycle is CC / TOP
Can divide the clock using CHx_DIV for each PWM channel

Our processor clock is 125 MHz

$period = \frac{1}{125 MHz}(DIV_{INT} + \frac{DIV_{FRAC}}{16})(TOP + 1)$


Assuming a 125 MHz clock speed, which values for TOP, CC, and DIV to get:
Period of 20ms
High time of 800us

- If possible select DIV first to make life easier
- If DIV = 125, then clock becomes 1MHz
- 20ms = 1/1MHz (TOP + 1)
- 0.020s = 1/10^6 Hz (TOP + 1)
- 0.020 * 10^6 - 1 = TOP
- 20000 - 1 = TOP
- TOP = 19999
- (800 / 20000) = CC / 19999 = 800

**Technical:**

8 different PWM slices in the RP2040
Each one can output to two GPIOs at a time

0A - GPIO0
0B - GPIO1
...
7A - GPIO14
7B - GPIO15
0A - GPIO16
0B - GPIO17
...
6A - GPIO28
6B - GPIO29

**Steps:**
1. Pull PWM out of reset
	`set_bit(RESETS_BASE, 1 << 14)`
	`clear_bit(RESETS_BASE, 1 << 14)`

2. Choose a pin and...
	- Configure pad for output
		`write_reg(PADS_BANK0_BASE + (PWM_PIN + 1) * 4, 0)`
	- Set FUNCSEL to 4
		`write_reg(IO_BANK0_BASE + (PWM_PIN * 8 + 4), 4)`
3. Set DIV
	`write_reg(PWM_BASE + CH#DIV, DIV << 4)`
4. Set TOP
	`write_reg(PWM_BASE + CH#TOP, TOP)`
5. Set Counter Compare A/B
	`write_reg(PWM_BASE + CH#CC, CC)` (shift by 16 if B)
6. Enable PWM
	`set_bits(PWM_BASE + CH#CSR, 1)`



### Shift Register Pins

| Pins    | Function | Details                    | Connect  |
| ------- | -------- | -------------------------- | -------- |
| 1-7, 15 | Q1-Q7    |                            | GPIO     |
| 8       | GND      |                            | GND      |
| 9       | Q7'      |                            | Shift R. |
| 10      | MR       | Master Reclear, active low | 3.3V     |
| 11      | SHCP     | Shift register clock pin   | GPIO     |
| 12      | STCP     | Storage register clock pin | GPIO     |
| 13      | OE       | Output enable, active low  | GND      |
| 14      | DS       |                            | GPIO     |
| 15      | Vcc      |                            | 3.3V     |

