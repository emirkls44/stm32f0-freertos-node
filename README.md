# STM32F0 FreeRTOS Node

FreeRTOS project on the STM32F0 Discovery board. Two LEDs blink at different speeds in separate tasks. Pressing the user button changes the speed of the blue LED, and every event is logged over UART.

## Demo

Two tasks blinking at different speeds:

https://github.com/user-attachments/assets/63c24105-79e1-4d38-89f9-491e368dc773

Button changes the blue LED speed:

https://github.com/user-attachments/assets/d61a8b3f-1d2f-46fa-97d3-efaa347d8297


UART log in the serial terminal:

https://github.com/user-attachments/assets/b0cc3083-8f6b-40b3-a4e5-8d43feea3aa2

## What it does

- Each LED runs in its own task, independent of the other.
- A button task sends press events to the LED task through a queue.
- UART logging is protected by a mutex so messages from different tasks don't mix.

## Hardware

STM32F0 Discovery and a CP2102 USB-TTL adapter. Connect CP2102 RX to PA9, TX to PA10 and GND to GND. Open a serial terminal at 115200 baud.

## Notes

- The HAL timebase was moved to TIM14 because FreeRTOS uses SysTick.
- The LED task waits on the queue with a timeout instead of `osDelay`, so it reacts to the button instantly.
- The board has only 8 KB of RAM, so the unused C heap was reduced to make room for UART.

## Build

Open the project in STM32CubeIDE, build and flash with the on-board ST-LINK.
