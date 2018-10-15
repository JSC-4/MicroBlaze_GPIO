
/*
 * GPIO_Test.c: simple test application
 *
 */

#include <stdio.h>
#include "platform.h"
#include "xil_printf.h" //this is not needed unless using UART
#include "xgpio.h"
#include "xparameters.h"

int main()
{
	XGpio input, output;
	int switch_data = 0;

	XGpio_Initialize(&input, XPAR_AXI_GPIO_0_DEVICE_ID);
	XGpio_Initialize(&output, XPAR_AXI_GPIO_1_DEVICE_ID);

	XGpio_SetDataDirection(&input,1,0xFFFF);
	XGpio_SetDataDirection(&output,1,0x0000);

    init_platform();

    while(1)
    {
    	switch_data = XGpio_DiscreteRead(&input, 1);
    	XGpio_DiscreteWrite(&output, 1, switch_data);
    }

    cleanup_platform();
    return 0;
}
