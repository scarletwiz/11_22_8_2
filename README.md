# Performance Measurement Test

This project will conduct a simple test for performance measurement.

##Performance Improvement Options
There are several methods that can be considered for performance improvement, including:

- Increasing MCU clock speed
- Improving communication speed
- Using DMA (which may not apply in some cases)
- Improving communication logic
- Please choose the appropriate method depending on the situation and implement it.

##Network Speed Test with Varying MCU Clock Speed
In this test, we will measure the network speed changes according to the MCU clock speed.

This project performs performance testing using the Nucleo429ZI board.
Note: The MAX main clock is 180. The communication speed is measured by adjusting the main clock, not the SPI.

Configuration
To adjust the communication speed, modify the following code in the board/NUCLEO_XXXX/mpconfigboard.h file:

```cpp
#define MICROPY_HW_CLK_PLLM (8)
#define MICROPY_HW_CLK_PLLN (336)
#define MICROPY_HW_CLK_PLLP (RCC_PLLP_DIV2)
#define MICROPY_HW_CLK_PLLQ (7)

```

To check if the configured function is applied correctly, add the following code to the port/stm32/main.c file:

```cpp
printf("\r\n hello f429, sys clock is %d \r\n", HAL_RCC_GetSysClockFreq());
```

Performance Measurement
Now measure the speed by adjusting the MCU clock as follows:

At too low of a clock speed, the speed will not be measured, and there is about a two-fold difference between 90MHz and 180 MHz.

### 45MHz: Not available
<p align="center">
  <img src="https://github.com/scarletwiz/11_22_8_2/blob/main/00.png?raw=true"/>
</p>

### 90MHz: 11.5 Mbit/sec
<p align="center">
  <img src="https://github.com/scarletwiz/11_22_8_2/blob/main/22.png?raw=true"/>
</p>

### 180MHz: 20.6 Mbit/sec
<p align="center">
  <img src="https://github.com/scarletwiz/11_22_8_2/blob/main/11.png?raw=true"/>
</p>

Note: Even if the MCU clock is high, 100% efficiency may not be achieved if it does not match the processing speed of the W5X00 chip.

Below are the specifications of the Nucleo board supported by W5300. Adjust according to the situation.

| Feature             | STM32-F207ZG            | STM32-F429ZI            | STM32-F439ZI            | STM32-F722ZE            | STM32-F756ZG            | STM32-F767ZI            |
|---------------------|-----------------------|-----------------------|-----------------------|-----------------------|-----------------------|-----------------------|
| Core                | ARM Cortex-M3          | ARM Cortex-M4          | ARM Cortex-M4          | ARM Cortex-M7          | ARM Cortex-M7          | ARM Cortex-M7          |
| Max. clock speed     | 120 MHz                | 180 MHz                | 180 MHz                | 216 MHz                | 216 MHz                | 216 MHz                |
| Flash memory        | 1 MB                   | 2 MB                   | 2 MB                   | 512 KB                 | 1.5 MB                 | 2 MB                   |
| SRAM                | 128 KB                 | 256 KB                 | 256 KB                 | 256 KB                 | 512 KB                 | 512 KB                 |
| GPIO pins           | 112                    | 168                    | 168                    | 100                    | 168                    | 216                    |
| ADC channels        | 24                     | 24                     | 24                     | 24                     | 24                     | 24                     |
| DAC channels        | 2                      | 2                      | 2                      | 2                      | 2                      | 2                      |
| USART interfaces    | 5                      | 4                      | 4                      | 4                      | 5                      | 5                      |
| SPI interfaces      | 4                      | 6                      | 6                      | 4                      | 4                      | 6                      |
| I2C interfaces      | 3                      | 4                      | 4                      | 4                      | 4                      | 4                      |
| Ethernet MAC        | Yes                    | Yes                    | Yes                    | Yes                    | Yes                    | Yes                    |
| USB OTG             | FS/HS                  | FS/HS                  | FS/HS                  | FS/HS                  | FS/HS                  | FS/HS                  |
| CAN interfaces      | 2                      | 2                      | 2                      | 2                      | 3                      | 3                      |
| Timers              | 14                     | 17                     | 17                     | 17                     | 17                     | 17                     |
| Real-time clock     | Yes                    | Yes                    | Yes                    | Yes                    | Yes                    | Yes                    |
| Operating voltage   | 2.0V - 3.6V            | 1.7V - 3.6V            | 1.7V - 3.6V            | 1.7V - 3.6V            | 1.7V - 3.6V            | 1.7V - 3.6V            |
| Pin Count           | 144                    | 144                    | 144                    | 144                    | 144                    | 176                    |
