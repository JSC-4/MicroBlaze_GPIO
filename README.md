# MicroBlaze with Nexys-4 DDR

This project is about using the Nexys-4 DDR, to create a MicroBlaze SoC and communicating with the UART to print "Hello World". 
This is the stepping stone for developing more complexed SoC based systems.

### Prerequisites

* MicroBlaze compatible FPGA board
* Vivado with license

## Getting Started

### Vivado

```
1. Create a new project. As no RTL sources are not used "Do not specify sources at this time" can be checked.
   Select the FPGA board used and finish building the project.
2. From the previous project a tcl sciprt of the MicroBlaze processor block design can be created in an
   executable file. This is done by going file->export->export block design. Save this file, open it in a text
   editing software, copy it's contents and paste it in the new projects tcl command line. This will regenerate
   the previous project. 
3. Add an AXI GPIO core, double click on the ip block, add dip switches in GPIO. Do the same for another AXI 
   GPIO core but add LEDs to GPIO. Run connection automation, validate the design, create a HDL wrapper 
   (if not already created) and generate bitstream.
4. Once bitstream is generated, go to file->export->export hardware and make sure INCLUDE BITSTREAM is checked.
5. File->Launch SDK
```

### SDK

```
1. When launched in SDK from Vivado, make sure the hw wrapper folder can be seen in the projext explorer window.
2. File->new->application project. Name the project and ensure the target harware is the same as the hw wrapper.
   In the next window pick Hello World template and finish.
3. Go to the helloworld.c (can change the name to something more appropriate) file from the application project 
   folder, in the src folder. To read GPIO three steps need to be done. 1) Initialise the GPIO, 2) Set data direction,
   3) Read data. Various online documents can describe this in detail, such as Xilinx's Writing Basic Software
   Application (see additional comments below).
4. Once this is done click program FPGA, then after right click the application project folder then run as->launch on 
   hardware (GDB). If using the UART terminal see this step the below.
5. Set up a serial terminal with the settings:
	COM Port: Check device manager
	Board Rate: 9600
	Data Bits: 8
	Stop Bits: 1
	Parity: None
```

## Additional Comments

- The previous project to create a MicroBlaze processor with a UART core is found [here](https://github.com/JSCBLOG/Microblaze_Hello_World)
- To change the buad rate, this can be done by clicking on the on the USB UART ip core in the block design.
- Link to Writing Basic Software Application [here](https://github.com/JSCBLOG/MicroBlaze_GPIO/blob/master/Writing%20Basic%20Software%20Application.pdf)
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



