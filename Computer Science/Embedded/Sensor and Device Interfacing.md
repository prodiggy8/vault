- Take multiple readings and filter, otherwise not reliable

1. Hardware (may take longer)
Take multiple values and return the average (in hardware)
Spend longer on single reading

2. Software: Averaging
Take multiple values and average them (in software)

3. Software: Running Average
Take one reading at a time and add to running average

4. ==Software: Exponential Filter==
==New reading is added to previous smoother result==
==$y_n=w \cdot x_n + (1 - w) \cdot y_{n-1}$==

==High $w$ will reduce smoothing and add reactivity to change==
==Low $w$ will produce smooth values but does not react quickly to change==

##### Interfacing

- Analog
- Binary (event was detected?)
- Serial (I2C, SPI, UART)
- Bit-banged (writing custom code to talk to the sensor)

### Serial

Sending bits one after another, instead of all at the same time

**Full duplex** communication: send and receive from the device **at the same time**

#### ==UART==
==Full-duplex==
==**RX, TX**==
==When to read bits? Both sides agree on timing==

- ==Default high==
- ==Set low to start==
- ==Send 8 bits==
- ==Set high to stop==

==**Parity bit:** option to send an extra bit==
	==1 if the number of 1s sent is odd==
	==0 if the number of 1s sent is even==

==**Settings:** need to configure speed (bps), Parity, # of bits, # of stop bits==

**UART in the RP2040**
- Two modules, accessible in two different sets of pins

#### ==SPI (Serial Peripheral Interface)==
==Full-duplex==
==RX/**MISO**, TX/**MOSI**, **CLK**==
==When to read bits? Master provides clock signal==

==SPI supports multiple slaves==
==All of them share CLK, TX, and RX pins with master==
==**Extra wire per device** is to select the device==

**SPI in the RP2040**
- Two modules, accessible in multiple different sets of pins

#### Inter-Integrated Circuit ($I^2C$)
==Half-duplex==
==**SDA, SCL**==
==When to read bits? Master provides a clock signal==

==**SDA:** Serial Data==
==**SCL:** Serial Clock==

- ==Supports many devices on the same two wires==
- ==Devices can be masters or slaves (often $1$ master and $\ge 1$ slaves)==
- ==Every connected device has an unique 7-bit address==

==Devices are configured and used based on:==
	==**Commands:** 8-bit value telling the device to do something==
	==**Registers:** 8-bit value at an 8-bit address==
		==could be written for device configuration==
		==could be read to get data==

- ==SCL and SDA are held high by the pull-up resistor until a device pulls them low==

==**Start a transmission:** master pulls SDA low while SCL is high==
==**Stop a transmission:** master allows SDA high while SCL is high==

##### ==Write==
1. ==Master sends start signal==
2. ==Master sends 7-bit device address==
3. ==Master sends 1-bit operation==
4. ==Slave sends ACK==
5. ==Master sends memory address or command==
6. ==Slave sends ACK==
7. ==Master sends 8-bits of data==
8. ==Slave sends ACK==
9. ==Master sends stop signal==

##### ==Read==
1. ==Master sends start signal==
2. ==Master sends 7-bit device address + W==
3. ==Slave sends ACK==
4. ==Master sends 8-bit address==
5. ==Slave sends ACK==
6. ==Master sends start signal (again!)==
7. ==Master sends 7-bit address + R==
8. ==Slave sends ACK==
9. ==Master pulses clock and slave sends 8-bits of data==
10. ==Master sends ACK==
11. ==Master sends stop signal==

- A write is done first to send the memory address, then a read is done!

Devices address? 
Memory addresses and commands?
Clock rate to use? 
Answer: **datasheet**

Sources:
1. Datasheet
2. Library for Arduino or RPI5
3. Generative AI

**$I^2C$ on the RP2040**

SDA_PIN, SCL_PIN
COMPASS_ADDR

1. ==Pull out of reset==
	==`set_bits(RESETS_BASE, 1 << 4)`==
	==`clear_bits(RESETS_BASE, 1 << 4)`==
2. ==Configure pads and pins==
	- ==Pull-up enabled, slew rate limited, Schmitt trigger enabled, input enable==
	==`write_reg(PADS_BANK0_BASE + (PIN + 1) * 4, 0b1001011)`==
	==`write_reg(IO_BANK0_BASE + (PIN * 8 + 4), 3)`==
3. ==Setup $I^2C$==
	- ==Master enable, slave disable, standard speed, 7-bit addressing==
	==`clear_bits(I2C1_BASE + IC_ENABLE, 1)`==
	==`write_reg(I2C1_BASE + IC_CON, 0b1010011)==
	==`set_cnts(125 MHz, 400 kHz)`==
	==`set_bits(I2C1_BASE + IC_ENABLE, 1)`==
4. ==Set peripheral address==
	==`clear_bits(I2C1_BASE + IC_ENABLE, 1)==
	==`write_reg(I2C1_BASE + IC_TAR, address)`==
	==`set_bits(I2C1_BASE + IC_ENABLE, 1)`==
5. ==To write:==
	==`write_reg(I2C1_BASE + IC_DATA_CMD, (1 << 10) | (0 << 9) | (0 << 8) | reg)`==
	==`write_reg(I2C1_BASE + IC_DATA_CMD, (0 << 10) | (1 << 9) | (0 << 8) | val)`==

	- ==Start with register, stop with data==
	- ==Bit 10 for RESTART==
	- ==Bit 9 for STOP==
	- ==Bit 8 for CMD (write mode is zero)==
6. ==To read:==
	==`write_reg(I2C1_BASE + IC_DATA_CMD, (1 << 10) | (0 << 9) | (0 << 8) | reg)`==
	- ==For each byte...==
		==`write_reg(I2C1_BASE + IC_DATA_CMD, (0 << 10) | (0 << 9) | (1 << 8) | reg)`==
		==`can_read = read_reg(I2C1_BASE + IC_STATUS) & (1 << 3) == 0`==
		==`data = read_reg(I2C1_BASE + IC_DATA_CMD) & 0xFF`==
	- ==On the last byte, send a STOP flag==
	