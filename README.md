# stm_mtr_controller

STM32CubeIDE bring-up project (`test_brd`) for a motor-controller test board based on the **STM32F446RE**, configured on a **NUCLEO-F446RE**.

## Peripherals configured (`test_brd.ioc`)

| Peripheral | Setup |
| --- | --- |
| TIM1, TIM8 | Advanced-control timers in PWM mode 1 for complementary gate drive. Prescaler 0, period 65535, dead time 0, break disabled |
| CAN1 | Normal mode, prescaler 16 |
| USART2 | 115200 baud (the Nucleo ST-LINK virtual COM port) |
| GPIO | PA5 (on-board LED LD2) |

## Current behaviour

`main.c` initializes the peripherals, then loops once a second: toggle PA5 and send `Hello World !!!` on USART2. The PWM timers are initialized but not started, and CAN is configured but unused.

## Build

1. Open the folder in STM32CubeIDE (`.project` / `.cproject` are included).
2. Build the `Debug` configuration and flash with the `test_brd Debug.launch` profile.
3. Open a terminal on the ST-LINK COM port at 115200 8N1.

Regenerate code from `test_brd.ioc` in CubeMX and keep edits inside the `USER CODE` blocks. Build output (`Debug/`) is not tracked.

## Next steps

- Start PWM channels (`HAL_TIM_PWM_Start` / `HAL_TIMEx_PWMN_Start`) and set the carrier period and dead time for the gate driver.
- Bring up the CAN traffic.
