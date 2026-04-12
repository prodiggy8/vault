Interrupt Service Routine is a function, takes no argument and returns nothing

Need to add to Interrupt Vector Table (pointers, stored in ROM)

`#[link_section = ".vector_table.interrupts"]`
`#[no_mangle]`
`pub static __INTERRUPTS: [unsafe extern "C" fn(); 26]`
`pub extern "C" fn IO_IRQ_BANK0() {}`

1. ==Check the datasheet to learn how to use==
2. ==Write ISR and add to table==
3. ==Enable the interrupt in INTE (interrupt enable)==
4. ==Clear existing interrupts in INTR (interrupt raw status)==
5. ==Enable interrupt in NVIC_ISER (interrupt set enable)==

**NVIC:** Nested vectored interrupt controller -> enables interrupt in Cortex-M0 core
**INTE** -> tells the peripheral itself to trigger interrupt given event

In ISR:
1. Check which interrupt was fired
2. (Do what you need to do)
3. Clear the interrupt in INTR

**CODE!!**

INPUT INTERRUPTS (always on IO_BANK0_BASE)

==`write_reg(IO_BANK0_BASE + 0x104, 1 << 30)`==
104 -> PROC_INTE1

INTE0 -> 1-7
INTE1 -> 8-15
INTE2 -> 16-23
INTE3 -> 24-29

Specific bit (30): specifies scenario and GPIO
==Level high -> whenever 1==
==low -> whenever 0==
==edge high -> from 0 to 1==
==edge low -> from 1 to 0==

==`write_reg(IO_BANK0_BASE + 0xf4, 1 << 30)`==
Write to INTR1 to clear pending interrupt
WC in datasheet -> write 1 to clear
needs to be cleared again in the Service Routine


==`write_reg(NVIC_ISER, 1 << 13)`==
enable IO_BANK0 interrupt in NVIC
Interrupt control, for GPIO is always 13

==`(read_reg(IO_BANK0_BASE + 0x124) & 1 << 30) != 0`==
reads from PROC0_INTS1 (status)

There exists proc0 and proc1 registers because there are two cores
(different INTE and INTS)

TIME INTERRUPTS

4 alarms (4 interrupts)
Only lower 32 bits of the timer
To enable:

1. Write time to fire to ALARM0
	- ==Will fire when TIMELR == ALARM0==
	- ==Read TIMELR, add time wanted, then write to ALARM0==
	- ==`write_reg(TIMER + 0x14, TIME)`==
2. ==Write to INTE to enable==
	- ==`write_reg(TIMER + 0x38, 1 << alarm)`==
3. ==Clear pending ALARM0 interrupts in INTR==
	- ==`write_reg(TIMER + 0x34, 1 << alarm)` WC==
4. ==Enable in NVIC_ISER==
	- ==`write_reg(NVIC_ISER, 1 << interrupt)` (0-3 for alarms)==
5. ==IN THE HANDLER==
	1. ==set alarm time again, it does gets deactivated!==
	2. ==ack in INTR: `write_reg(TIMER + 0x34, 1 << alarm)`==


==When interrupt happens:==
- ==registers saved to stack (r0-r3, r12, LR, PC, PSR [flags, etc]), rest is not==
- ==address for ISR loaded==
- ==LR set to special value for ISR (top 24 bits FF, next 7 specify:==
	- ==Main execution 0xF9==
	- ==Other ISR: 0xF1==

==Upon return:==
- ==BX LR==
- ==Processor notices the upper bits, pops 8 registers from stack==
- ==Checks next bits to see if returns to main execution or ISR==

==The lower interrupts in IRQ have priority over high (will interrupt an interrupt if triggered)==

##### Using mutable stuff in ISR

==`Struct State {}`==
==`static SHARED_DATA: Mutex<RefCell<Option<State>>> =`==
	==`Mutex::new(RefCell::new(None))`==

==In the main routine, we initialize it:==

==`cortex_m::interrupt::free(|cs| {`==
	==`*SHARED_DATA.borrow(cs).borrow_mut() = Some(State {});`==
==`})`==

==In the ISR:==

==`cortex_m::interrupt::free(|cs| {`==
	==`if let Some(ref mut state) = *SHARED_DATA.borrow(cs).borrow_mut() { ... }`==
==`}`==


#### State Machine for IR signal

`State = { state, last_time, input, checksum, bit_index }`

`enable_edge_low()`
`clear_pending()`
`enable_on_nvic()`

`GPIO_ISR {`
	`elapsed = current_time - last_time`
	`if is_interrupt and elapsed > 700 {`	
		`if state is HEADER`
			`if elapsed in HEADER_INTERVAL`
				`state = RECEIVING`
				
		`if state is RECEIVING`
			`bit = 1 if elapsed in ONE INTERVAL else 0`

			`if bit_index < 8 { add bit to input }`
			`elif bit_index < 16 { add to checksum }`
			`elif bit_index < 24 { add to input }`
			`else { add to checksum }`

			`if bit_index > 31 {`
				`if input = checksum.reverse() { show_on_leds(input) }`
				`state = HEADER`
			`}`
			
	`}`
	`clear_pending()`

`}`