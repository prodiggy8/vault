Board Crate
	e.g. rp_pico
	{
	HAL
		Interface for various standardized interfaces
		Uses the PAC
		{
			Peripheral Access Crate	
					Thin layer over control registers
		}
	}

**Blinky PAC**
`pub static BOOT2: [u8; 256] = rp2040_boot2::BOOT_LOADER_W25Q080;`

`let mut pac = hal::pac::Peripherals::take().unwrap();`
`let mut watchdog = hal::Watchdog::new(pac.WATCHDOG);`
`let clocks = hal::clocks::init_clocks_and_plls(`
        `12_000_000u32,`
        `pac.XOSC,`
        `pac.CLOCKS,`
        `pac.PLL_SYS,`
        `pac.PLL_USB,`
        `&mut pac.RESETS,`
        `&mut watchdog,`
`)`
`.unwrap();`
`let mut timer = rp2040_hal::Timer::new(pac.TIMER, &mut pac.RESETS, &clocks);`
`pac.PADS_BANK0`
        `.gpio(25)`
        `.write(|w| w.od().clear_bit().ie().clear_bit());`
`pac.IO_BANK0`
        `.gpio(25)`
        `.gpio_ctrl()`
        `.write(|w| w.funcsel().sio());`
`pac.SIO`
        `.gpio_oe_set()`
        `.write(|w| unsafe { return w.bits(1 << 25) });`

`pac.SIO.gpio_out_set().write(|w| unsafe { w.bits(1 << 25) });`
`timer.delay_ms(1000);`
`pac.SIO.gpio_out_clr().write(|w| unsafe { w.bits(1 << 25) });`
`timer.delay_ms(1000);`

**Blinky HAL**
Same up to timer.

`let pins = hal::gpio::Pins::new(`
        `pac.IO_BANK0,`
        `pac.PADS_BANK0,`
        `sio.gpio_bank0,`
        `&mut pac.RESETS,`
`);`
`let mut led = pins.gpio25.into_push_pull_output();`
`led.set_high().unwrap();`
`timer.delay_ms(1000);`
`led.set_low().unwrap();`
`timer.delay_ms(1000);`

**Reconfiguring:**
`let mut led: Pin<Gpio25, FunctionSio<SioOutput>, PullNone> = pins.gpio25.reconfigure();`

_ can be used in place of Gpio25 for HAL to infer
_ can be used in place of PullNone and PullDown (default) will be applied

Type DynPinId is a generic pin, good for function arguments
SioInput can be used, reading can be done with is_high() and is_low()

**I2C**
`let sda_pin: Pin<Gpio2, FunctionI2C, PullUp> = pins.gpio2.reconfigure();`
`let scl_pin: Pin<_, FunctionI2C, _> = pins.gpio3.reconfigure();`

`let mut i2c = hal::I2C::i2c1(`
	`pac.I2C1,`
	`sda_pin,`
	`scl_pin,`
	`400.kHz(), // need hal::fugit::RateExtU32 for .kHz() to work`
	`&mut pac.RESETS,`
	`&clocks.system_clock,`
`);`

`i2c.write(ADDRESS, &[REG, value]);`
`i2c.write_read(ADDRESS, &[REG], &mut res);`

**ADC**
`let mut adc = hal::Adc::new(pac.ADC, &mut pac.RESETS);`
`let adc_pin = hal::adc::AdcPin::new(pins.gpio26).unwrap();`
`adc.free_running(&adc_pin);`

`let adc_reading: u16 = adc.read_single();`