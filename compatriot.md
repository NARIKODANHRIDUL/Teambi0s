***
# **bi0s Hardware**
_Narikodan Hridul_
***
# **CompatrIoT** 
##### Project Proposal

***

### **UART**
##### **Universal Asynchronous Reciever-Transmitter**
Hence no clock will be involved in the UART

#### UART Connections
it is a oneway communication method, so it need 2 wires for to and fro communication
Tx pin of first board is connected to Rx of second and vice versa. And the ground pin will connected to a common ground.
   It determine howmany times it check for bits.If 4 High(1) is given together how will we differentiate with one long High(1), there comes baud rate.
![](https://github.com/NARIKODANHRIDUL/RANDOM-1/blob/main/uart.jpg?raw=true)

#### BAUD RATE 
It is a measure of the speed of data transfer, expressed in bits per second
**Standard baud rate** :  2400, 4800, 9600, 256000


#### UART CONFIGURATION
1. simplex - one way communication
2. half duplex - two way communication but not in same time
3. full duplex - two way communication but in same time

#### UART Advantage
1. only uses two wires
2. no clock signal required
3. Provider network detection by parity bit check
4. Cost and size will be much less when compared to the parellel communication

#### UART Disadvantages
1. Max size of data frame is 9 bits
2. Doesn't support mulitple master slave or mulitiple master system
3. Limited speed is the bottleneck for the application which require highter data transmission rate

#### Packet structure of UART
**`[ Start Bit ]`** - **`[ Data Frame ]`** - **`[ Parity Bit ]`** - **`[ Stop Bit ]`** 
> **Start Bit**
Idle state of signal is high. To start, this bit is set to low

> **Data Frame**


> **Parity Bits**
Its an optional bit used for checking error
 Parity bit = 0 => number of "one" in data frame is even
 Parity bit = 1 => number of "one" in data frame is odd

>**Stop bits** 
Bit is set to high to indicate end of data frame

---
---
## **JTAG**
#### Joint Test Action Group 
Processors often use JTAG to provide access to their debug/emulation functions and all FPGAs and CPLDs use JTAG to provide access to their programming functions.
> **FPGA** - Field Programmable Gate Array.
  **CPLD** - Complex Programmable Logic Device 

**JTAG** is a common hardware interface that provides your computer with a way to communicate directly with the chips on a board. It is an industry standard for verifying designs and testing printed circuit boards after manufacture. 

#### Advantages of JTAG
- allows the user to stop excecution at any time
- allows you to manipulate and examine the status of a supported AVR while it is running in a circuit. 
- shorter test times
- higher test coverage
- increased diagnostic capability
- lower capital equipment 

---
##### Fucntional Test

An old Way of testing electronics system .A functional test emulates or simulates a product's operational environment to check its correct functionality. 
##### Drawbacks
* it may be difficult to replicate a functional setup that sufficiently mimics the end application.
* sufficiently testing the operational space of systems, with even moderate complexity, can be very difficult.

---

##### Structural Testing
An alternative for testing functional operation is Structural testing. This method tests individual partitions instead of looking at the system as a whole. It enables a more thorough testing that can verify corner cases which are difficult to access using functional test only.
##### Drawbacks
* Gaining access to internal nodes is a challenge.
    * One traditional method for accessing internal nodes is employing a fixture with multiple electrical contacts, touching down on exposed metallic pads. This fixture is commonly called a "bed of nails."
    * these fixtures are costly to fabricate and difficult to make a solid connection when there are many points to access simultaneously.
*  This method becomes more problematic when circuit technology shrinks, with a higher reliance on multiple layered boards.
---
#### Boundary Scan
Boundary scan is an ingenious approach to structural testing that overcomes these challenges. Instead of relying on mechanical connections for access, it adds dedicated test circuitry to the system's ICs, using special registers inserted at the I/O pins.
These registers can observe data on the I/O pins, and they can be used to override drive signals, providing test stimulus to the circuit. It is this combination of stimulating and observing internal nodes that provides a powerful mechanism for accurate structural testing.![](https://github.com/NARIKODANHRIDUL/RANDOM-1/blob/main/boundaryscan.jpg?raw=true)
To gain test access to these registers, there is a separate serial data chain, independent of the functional paths as shown in the above figure.

##### Typical boundary scan registers can have four different types of 
**`1. Passing Data :`** operation allows **_data to pass_** through the registers transparently, without modification. This is the typical state of the circuit during normal functional operation.
 **`2. Capturing Data:`** It **_captures data_** coming into the register, without changing its value. This is how test data is observed.
**` 3. Updating :`** It **_updates_** the output of the register, disregarding the data coming into the register. This is how stimulus is applied to the circuit under test.
**` 4. Serial Shift :`** It enable test access to each register. **_Shifting_** the test response from the boundary registers into an off-board register allows it to be scanned and compared to the expected response.

#### Problems faced by JTAG - Boundary Scan
 > When the test department decides to utilize boundary scan, they need to work with the board developers to add it to the design.
 
 > Next, IC manufacturers need to have boundary scan registers built into the devices they provide. 
 
 >  Finally, someone needs to provide software tools that can gather the information from these different sources and create a program.
 
> **A standard has been developed for boundary scan. Established in 1990 by a team of industry representatives called the "Joint Test Access Group," it became the IEEE 1149.1 standard. The standard is often referred to simply as "JTAG."**

--- 
**`#`** **JTAG has moved beyond the chip boundary to access the chip's own test structures such as built-in self-test for verifying internal memory and logic.**
**`#`** **JTAG has become a preferred method for field testing because it allows circuit access without disassembly.**
**`#`** **Design debugging is another application for JTAG because it enables an unobtrusive way to access the state of the system.**

---
---
## **I2C**
#### Inter Integrated Circuit
It is also refered to as IIC. It provides a simple and robust serial communication between a peripheral device and a microcontroller.
![](https://raw.githubusercontent.com/NARIKODANHRIDUL/RANDOM-1/main/i2c.jpg)

* It is a **`synchronous protocol`** that allows a master to initiate communication with a slave device 
* I2C protocol is a **`master-slave communication`** with the master providing the clock which effectively becomes the data transfer rate or clock frequency 
* It is a **`bi-directional bus`** meaning the master can write to the slave and read from the slave
* It is a **`serial bus`** which means data is clock or shifted bit by bit and there are two bus lines **SCL (serial clock) and SDA (serial data)**

#### I2C Speed Chart
| Speed Category         | Clock Frequency | Bus direction  |
|:----------------------:|:---------------:|:--------------:|
|Standard-Mode(SM)       | Up to 100 KHz   | Bidirectional  |
| Fast-Mode(FM)          | Up to 400 KHz   | Bidirectional  |
| Fast-Mode Plus(FM+)    | Up to 1 MHz     | Bidirectional  |
|High-Speed Mode(HS)| Up to 3.4 MHz   | Bidirectional  |
| Ultra-Fast Mode (UFM)  | Up to 5.0 MHz   | Unidirectional |

Out of these Standard-Mode, Fast-Mode, Fast-Mode Plus are the most commonly used as they can be implemented easily

![](https://raw.githubusercontent.com/NARIKODANHRIDUL/RANDOM-1/main/i2cexample.jpg)
Here R1 and R2 are the pull-up resistors which are required for I2C devices to communicate properly. This is because I2C protocol works on the premise that the SCL and SDA bus lines are open drain or open collector

#### I2C Advantage
 I2C devices compared to other protocols are slightly **lower costs** to manufacture 
**`#`** due to the **lower number of logic gates** needed to build the I squared C interface
**`#`** it **only takes 2 pins** to implement which also translates to low cost 

This **lower cost** has made I2C the most common and **widely used serial bus** across most applications including **IOT,  consumer electronics, industrial equipment, automotive and aerospace**


## **SPI**
#### Serial Peripheral Interface
It was developed by Motorola to provide **full duplex synchronous serial communicarion** between **master and slave devices**. For every clock cycles one bit is transfered. A communication protocal thast uses **4 wires**.

![](https://raw.githubusercontent.com/NARIKODANHRIDUL/RANDOM-1/main/SPI.jpg)

##### 4-wire SPI devices have four signals:
* Clock (SPI CLK, SCLK)
* Chip select (CS)
* main out, subnode in (MOSI)
* main in, subnode out (MISO)

**`#`** The device that generates the clock signal is called the main. 
**`#`** Data transmitted between the main and the subnode is synchronized to the clock generated by the main. 
**`#`** SPI devices support much higher clock frequencies compared to I2C interfaces. 
**`#`** Users should consult the product data sheet for the clock frequency specification of the SPI interface.
**`#`** SPI interfaces can have only one main and can have one or multiple subnodes. Above figure shows the SPI connection between the main and the subnode.


#### Advantages
* No start and stop bits, so the data can be streamed continuously without interruption
* No complicated slave addressing system like I2C
* Higher data transfer rate than I2C (almost twice as fast)
* Separate MISO and MOSI lines, so data can be sent and received at the same time

#### Disadvantages
* Uses four wires (I2C and UARTs use two)
* No acknowledgement that the data has been successfully received (I2C has this)
* No form of error checking like the parity bit in UART
* Only allows for a single master




***
##  **THANK YOU 😃**
***
