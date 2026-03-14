# JTAG, SPI & UART details.

The QCA7420 chip used in the Trendnet TPL-406e powerline adapters is reported to have [GPIO (General-Purpose Input/Output)](https://www.youtube.com/watch?v=zwdmmetAL84), [JTAG (Joint Test Action Group)](https://www.youtube.com/results?search_query=what+is+jtag), [SPI (Serial Peripheral Interface)](https://www.youtube.com/shorts/P-NLGA8gW18) and [UART (Universal Asynchronous Receiver-Transmitter)](https://www.youtube.com/shorts/P-NLGA8gW18) capabilities.

An online search for its technical docs returned a blank but a technical doc for the QCA7005 chip was found (link below). 

https://www.scribd.com/document/845052654/qca7005-enhanced-industrial-homeplug-green-phy-single-chip-solution-data-shee

Its quite likely the GPIO, JTAG, SPI & UART information detailed in the above document is identical to the QCA7420 chip and much of the mode of operation, so the following QCA7005 information is documented below for those that want to explore those direct communication methods with the QCA7420 chip. More detailed information can be found by reading the above document.

The QCA7005 uses an embedded [ARM926 processor](https://www.youtube.com/watch?v=_LSPh-KWGhk) which has GPIO, JTAG, SPI and UART capabilities. It requires firmware (FW) be loaded from an external device or host processor source.

So its quite likely for the above reason and others, namely Arm cpu's seem to be efficient and value for money cpu choice, and so if the CPU offer's these facilities, its almost certain you will be able to access the device using these methods.

Firmware must be loaded to enable data transfer/processing to and from the mains powerline. 

The firmware does not reside on-chip, the QCA7005 boot sequencing requires the ability to download configuration and code from an external device like NVM (flash memory) using the Master SPI bus or the SPI Slave bus port from a host processor. See Boot Options Page 44 in the above document for more info.

Absolute Maximum Ratings can be found on Page 47 of the above document because you dont want to blow your chip up now.

Recommend Operating conditions & Power supply Requirements on Page 48.

Communication Protocol: The QCA devices, when operating via SPI, often use a specific ["Ethernet over SPI" protocol](https://www.kernel.org/doc/Documentation/devicetree/bindings/net/qca-qca7000-spi.txt), requiring drivers (such as qca7000) that define the device in the host's device tree.

Bootloading: SPI is used for loading firmware (PIB and firmware) into the device's RAM during startup using tools like ```plcboot```.

The QCA7005 functions are executed in firmware running on the embedded ARM926 CPU, supported by DMA hardware, and on-chip SDRAM for runtime code and data store. GPIO are available for application I/O and to drive LED's directly to indicate PLC link status, as well as to indicate user reset or network attach events. A dedicated QCA7005 IC sub system is responsible for power management functions.

Zero Cross. The QCA7005 has an analogue amplified circuit that detects when the 50Hz or 60Hz AC powerline voltage crosses through to zero volts. The synchronisation info is used by software algos to optimise powerline communications in high noise conditions.


GPIO read at power on to configure the operation of the QCA7005.
```
Boot from NVM				60	GPIO_0		High (1) indicates boot code loads from NVM flash device on the Master SPI bus port.	
Boot from SPI Slave bus		61	GPIO_1		Must be Pulled Low (0) for all QCA7005 applications.
SPI Slave mode				62	GPIO_2		Low (0) = Legacy command/data. 1 = Burst command/data.
User I/O 					63	GPIO_3		Not Defined during Boot Up.
```


## Serial Interfaces

With the text on the QCA7005 chip in the normal Left to Right position so you can read it properly, Pin 1 is the 1st pin on the top of the left side, the pins then increment by 1 as they go down the left side, from left to right on the bottom side, from bottom to top on the right side and then from right to left on the top side. In other words, the pin number's increment in a counter clock-wise, ie reverse or backwards direction to a [normal analogue clock](https://www.youtube.com/shorts/SL1RD-09dVM). 

### UART - Universal Asynchronous Receiver-Transmitter

Speeds up to 115,000 baud supported over 4 pins, TX & RX Data, RTS & CTS (optional use)

| Pin | Type | Direction | Note |
|-----|------|-----------|------|
| 14 | Serial In | In | |
| 15 | Serial Out | Out | |
| 16 | CTS (Clear to Send) | In | |
| 19 | RTS (Request To Send) | Out | |


### SPI - Serial Peripheral Interface Master (for NVM Flash)

Standard 4 wire Motorola Mode 3 SPI Protocol + Interrupt pin.
Max data rate is approximately 5.4Mbps UDP in SPI Slave mode.
8, 16 & 32 bit data framing, 16bit recommended.
SPI controller DMA support for large data frame sequences.
Burst slave mode is recommended. 
Legacy mode (not recommended) requires external reset or QCA7005 power cycle.

| Pin | Type | Direction | Note |
|-----|------|-----------|------|
| 03 | SPI_DI (Serial Data In) | In | The QCA7005 Master SPI_DI is used to transfer firmware into the QCA7005. SPI_DI is latched on the rising edge of the SPI_CLK. Motorola Mode 3 SPI Protocol aka SPI Mode 3 |
| 65 | SPI_CS_L	(Serial Chip Select (Active) Low ) | In | SPI_CS_N is the chip select used to enable the serial boot flash. This signal is tri-stated and held high with a weak internal pull up while RESET_L is asserted. |
| 66 | SPI_DO (Serial Data Out) | Out |  SPI_DO is used to transfer serial data out of the QCA7005. SPI_DO is shifted out on the falling edge of the SPI_CLK. This signal is tri-stated and held low with a weak internal pull-down while RESET_L is asserted. |
| 67 | SPI_CLK (Serial Clock) | Out | SPI_CLK provides the SPI interface timing. Instructions, addresses or data present at SPI_DI are latched oon the rising of the SPI_CLK. Data on SPI_DO changes after the falling edge of SPI_CLK. This signal is tri-stated and held low with a weak internal pull-down while RESET_L is asserted. |

### SPI -  Serial Peripheral Interface Slave

SPI Slave command fields detailed in the document above on page 27.

| Pin | Type | Direction | Note | 
|-----|------|-----------|------|
| 14 | SPI_MOSI (Master Out Slave In) | In | |
| 15 | SPI_MISO (Master In Slave Out) | Out | | 
| 16 | SPI_CS (Chip Select) | In | | 
| 19 | SPI_CLK (Clock) | Out | |
| 20 | SPI_SI (Slave Interrupt) | Out | | 


### JTAG - Joint Test Action Group


| Pin | Type | Direction | Note |
|-----|------|-----------|------|
| 22 | TDI (Test Data In) |	In	| 10K to GND for normal operation |
| 23 | TCK (Test Clock)	| Out |	10K to GND for normal operation |
| 24 | TDO (Test Data Out) | I/O | 3.3K to GND for normal operation |
| 25 | TMS (Test Mode Select) | In | 10K to GND for normal operation |
| 26 | RTCK	(ARM based debugger Return Test Clock) | Out | 	Leave unconnected for normal operation |
| 27 | TRST_L (Test ReSeT (Active Low)) | In | 10K to GND for normal operation |


### GPIO 

| Pin | Type | Direction | Note | 
|-----|------|-----------|------|
| 14 | Shared_GPIO_8 | I/O | | 
| 15 | Shared_GPIO_7 | I/O | |
| 16 | Shared_GPIO_6 | i/O | |
| 19 | Shared_GPIO_5 | I/O | |
| 20 | Shared_GPIO_4 | I/O | |
| 60 | GPIO_0 |	I/O	| GPIO_0 Sets mode at power on then becomes I/O | 
| 61 | GPIO_1 | I/O	| GPIO_1 Sets mode at power on then becomes I/O |
| 62 | GPIO_2 | I/O	| GPIO_2 Sets mode at power on then becomes I/O | 
| 63 | GPIO_3 | I/O	| GPIO_3 Sets mode at power on then becomes I/O | 
