# STM32 HAL Library Cheatsheet
## Using printf as hardware output

C
```c
int __io_putchar(int ch)
{
    (void)HAL_UART_Transmit(&huart6, (uint8_t*)&ch, 1, HAL_MAX_DELAY);

    return ch;
}
```