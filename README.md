# MicroBlaze with Nexys-4 DDR

This project is about using the Nexys-4 DDR, to create a MicroBlaze SoC and communicating with the UART to print "Hello World". This is the stepping stone for developing more complexed SoC based systems.

### Prerequisites

* MicroBlaze compatible FPGA board
* Vivado with license

## Getting Started

### Vivado

```
1. Create a new project. As no RTL sources are not used "Do not specify sources at this time" can be checked.
   Select the FPGA board used and finish building the project.
2. Create a new block design. Add System Clock from Board tab, then Reset to the block design. Make sure to have 
   RESET TO ACTIVE LOW on reset pin AND clocking wizard. Add Microblaze IP and run block automation with default 
   settings. Add USB UART and run block automation. Lastly click validate design.
3. Go the the sources tab and right click the block design file under Design Sources and click create HDL wrapper,
   letting Vivado manage wrapper and auto-update. Click generate bitstream, which will also do synthesis and 
   implementation.
4. Once bitstream is generated, go to file->export->export hardware and make sure INCLUDE BITSTREAM is checked.
5. File->Launch SDK
```

### SDK

```
1. When launched in SDK from Vivado, make sure the hw wrapper folder can be seen in the projext explorer window.
2. File->new->application project. Name the project and ensure the target harware is the same as the hw wrapper.
   In the next window pick Hello World template and finish.
3. Go to the helloworld.c file from the application project folder, in the src folder. To show the "Hello World" 
   print multiple times, it can be put in an infinite for or while loop.
4. Click program FPGA, then after right click the application project folder then run as->launch on hardware (GDB).
5. Set up a serial terminal with the settings:
	COM Port: Check device manager
	Board Rate: 9600
	Data Bits: 8
	Stop Bits: 1
	Parity: None
```



## Additional Comments

- To change the buad rate, this can be done by clicking on the on the USB UART ip core in the block design.
- Can also add the MicroBlaze IP first and then the clocking wizard. After generate all the needed cores from running the block automation. The reset will need to be changed to active low in the clocking wizard. Possible error when generating the bitstream, which can be fixed by deleting the clocking wizard and adding it again.

## Issues and Bugs

**MicroBlaze held in reset:**<br/>
	Error: On the software side when running the software on the FPGA, an error message comes up saying "Error while launching 		       program: Cannot stop MicroBlaze. MicroBlaze is held in reset".<br/>
	Fix: The block design needs to be changed to have the reset as ACTIVE LOW. This is also needs to be set in the clocking wizard 		     ip core. 

**SDK crashing:**<br/>
	Error: SDK crashes and when relaunched the screen will show the error message: Plug-in org.eclipse.cdt.ui was unable to load 	            class org.eclipse.cdt.internal.ui.editor.CEditor. <br/>
	Fix: Open SDK from windows NOT Vivado and open it to the project .sdk folder.

**SDK launching internal error:**<br/>
	Error: When lauching SDK from Vivado an error message will pop up saying "The folder... .metadata" is read only.<br/>
	Fix: Remove any spaces in the file names of ALL connected folders.

## Built With

* [Vivado](https://www.xilinx.com/products/design-tools/vivado.html) - The software used
* [Nexys-4 DDR](https://store.digilentinc.com/nexys-4-artix-7-fpga-trainer-board-limited-time-see-nexys4-ddr/) - The hardware used

## Website

[JSCBLOG](http://jscblog.com/)



