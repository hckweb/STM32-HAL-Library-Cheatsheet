# STM32 HAL Library Cheatsheet
### Using printf as hardware output

```c
int __io_putchar(int ch)
{
    (void)HAL_UART_Transmit(&huart6, (uint8_t*)&ch, 1, HAL_MAX_DELAY);

    return ch;
}
```

### Interrupt Handler in FreeRTOS

```c
//on global namespace
static SemaphoreHandle_t bin_sem = NULL;

//on setup
void setup(void) {
    bin_sem = xSemaphoreCreateBinary();
}

//on ISR function
void ISR_From_Blabla(Something_t* thing) {
    BaseType_t task_woken = pdFALSE;
    xSemaphoreGiveFromISR(bin_sem, &task_woken);
}

//on handler task
void ISR_Handler(void const* argument) {
    xSemaphoreTake(bin_sem, portMAX_DELAY);
    //Some interrupt stuff
}
```