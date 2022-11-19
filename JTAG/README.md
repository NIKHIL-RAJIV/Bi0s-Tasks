# JTAG
  
  JTAG , commonly referred to as boundary-scan was developed for validating proper assembly of components on PCB boards in the 1990s. JTAG is mainly used by IC manufacturer at the developing and testing stage as well as giving access to the internal subsystem of IC,  
**TAP Controller** 
TAP Controller is the main component, a finite state machine which is responsible for the behavior of JTAG boundary scan logic in the chip. It is responsible for controlling the JTAG chain and the TAPs. It is also responsible for the communication between the JTAG chain and the host. The TAP Controller is a finite state machine (FSM) that is controlled by the host. The TAP Controller is connected to the TAPs through a serial interface. The TAP Controller is responsible for the following:
 Generates signals to control the operation of the 
 1. Test data registers
 2. Instruction registers
 3. Associated circuitry  

The TAP controller finite machine has two main paths for setting and retrieving information from either the instruction register or the data register

**Test Access Port (TAP)** 
- This port gives easy access to test functions built into a component. It has four input ports, i.e., Test Clock (TCK), Test Mode Select (TMS), Test Data Input (TDI), Test Reset (TRST) (optional), and one output port, i.e., Test Data Output (TDO). Here, TCK, TMS and optional TRST are broadcast signals, whereas TDI builds serial chain, in which test signals are injected and get test output signals at TDO port. Only these four pins are required to inject test signals on PCB regardless of the number of components on PCB.
      
**One or more data register(s)**   
- These registers are used to read-out information in the component. There are a minimum of two mandatory registers described in this standard, i.e., Boundary Scan and bypass registers. There are data registers which contain “device ID” and are known as “idcode” register.


**Instruction Register**
- The “Instruction register” decides on the operation mode of the Boundary Scan IC. The IEEE standard has three main instructions (modes): BYPASS, SAMPLE/PRELOAD, and EXTEST.

## JTAG Exploitations

Exploitation of JTAG Using Physical Pin Modification:
- The TDI pin is used to inject test signals or secret data into “n” number of devices, which are connected in series such as memories, sequential or combinational circuits, etc. If the tester or user is injecting some secret data into the TDI pin, then that data can be sniffed by a device such as memory, controller, etc. that is already present in that series of devices. This is called a “sniffing attack”.

Exploitation of JTAG Using Software:

- By using AVR ICE JTAG programmer to dump and retrieve HEX code. The open source programs such as linux based standard GDB debugging tool, UISP, avr-objcopy and avr-tool are used to got object file through serial interface connected to the PC. The Hex converter tool is used for reverse conversion of the assembly code. Generally, SRAM is considered as the safest among all memories to store keys and sensitive information due to its volatile nature. 

Exploitation Using JTAGulator Tool:
 
- It is one of the important tasks to find open pinouts first that are kept by manufacturers on PCB board for future debugging and improvement because PCB manufacturers usually hide JTAG interface points from user to provide basic security rather than exposing it directly. The JTAGulator, is an open source hardware tool developed by developer Grand . Here one  explores the open pins that are indirectly available on PCB to normal user through brute force attack. Once the hacker gets to know the pinout from PCB board through manual inspection, then the attacker can easily get access to the firmware or bootloader. JTAGulator board assists all users in identifying OCD (On Chip Debug) interfaces from test points or components pads which are available on PCB boards. The JTAGulator tool can be connected to a PC.  
      
Exploitation Using Interrupt-Oriented Bugdoor Programming Method:

- The concept called “bugdoor”. “Backdoor” is a popular term used in software industry for a special code snippet left in the program to secretly control future debugging. However, if attacker gives proper inputs to the target program in the device, then the attacker can inject malicious code in the firmware causing unintentional behaviour of device or stealing sensitive data. Generally, server exploitation considers getting shell (root) access, whereas microcontroller firmware access could be more devastating, since attacker can change the device behaviour, steal protection keys and more. It can go unnoticed by the owner of the device so that attacker can continue stealing data and can keep a watch on the device.
One can perform three different exploits by writing a simple firmware on a microcontroller to generate timely nested interrupts. First, the state accumulation exploit acquires state changes information when interrupt occurs on target device, through which program behaviour change has been done. Second, the loop execution exploit changes memory contents by nesting interrupt loop. Third, the stack growing exploit is done when the target device receives continuous interruptions, in which stack contents grow by 2 bytes each time. 

Baseband Attacks: 
      
- There are three steps for exploitation: firmware acquisition, analysis of hardware and its components, and analysis of disassembled firmware. Here, the RealView ICE debugger is used in auto configuration mode to get all ARM related information. The hardware analysis is mandatory to identify the instruction set used in firmware. One has to follow static and dynamic analysis for firmware by using IDA Pro disassembler and Basnight are used to identify ARM functions. During the static analysis, the location of firmware images in volatile memory is identified where initial jump to the entry point of the firmware is occurred. During the dynamic analysis, firmware execution paths are identified by using JTAG interface through which memory breakpoints can be set and test read/write access. This JTAG interface can also dump memory and register values before PLC goes into fault state which helped understanding conditional flags of hardware status.
