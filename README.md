# STM32 LED Control with Timer Interrupt

This is a simple STM32 project that demonstrates how to use Timer2 interrupt to control LEDs connected to pins 12, 13, 14, and 15 on the STM32 microcontroller.

## Description

The project uses Timer2 to generate interrupts every 1 second. Each time the interrupt occurs, the LED connected to the corresponding pin (12, 13, 14, or 15) will be toggled, creating a sequential LED blinking effect.

## Getting Started

### Prerequisites

- STM32 microcontroller (tested on STM32F4xx series)
- STM32CubeIDE or a compatible development environment
- STMicroelectronics HAL library

### Hardware Connections

- Connect LEDs to pins 12, 13, 14, and 15 on the GPIO port.

### Running the Project

1. Clone or download this repository.
2. Open the project in STM32CubeIDE or your preferred development environment.
3. Build the project and flash it to your STM32 board.

## Code Explanation

The main logic for controlling the LEDs is implemented in the `TIM2_IRQHandler()` function, which is the Timer2 interrupt handler. It uses a counter variable to keep track of the number of interrupts and toggles the LEDs accordingly.

```c
// Code snippet from main.c
void TIM2_IRQHandler(void)
{
  count++;

  if (count == 1){
    HAL_GPIO_TogglePin(GPIOD, GPIO_PIN_12);
  }
  else if (count == 2){
    HAL_GPIO_TogglePin(GPIOD, GPIO_PIN_13);
  }
  else if (count == 3){
    HAL_GPIO_TogglePin(GPIOD, GPIO_PIN_14);
  }
  else if (count == 4){
    HAL_GPIO_TogglePin(GPIOD, GPIO_PIN_15);
  }
  else{
    count = 0;
  }

  HAL_TIM_IRQHandler(&htim2);
}
