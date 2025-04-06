Szabo Cristina-Andreea
# E-book Reader
The project is built around the ESP32-C6-WROOM-1-N8 microcontroller, which integrates Wi-Fi and Bluetooth Low Energy functionality. It is responsible for managing communication between the connected components, sensor data acquisition, and display handling. Below are the key components and their connections to the ESP32-C6, with detailed descriptions of the pins used, communication protocols, and power management considerations.

## Block Diagram:
## BOM - Bill of materials

## Hardware Description:
- ESP32-C6-WROOM-1-N8: The heart of the system, providing Wi-Fi and BLE capabilities for wireless communication.
- BME688: An environmental and air quality sensor that measures temperature, humidity, pressure, and gas. It communicates with the ESP32 via the I²C protocol.
- DS3231SN: A high-precision Real-Time Clock (RTC) module, connected via I²C for accurate timekeeping.
- MAX17048: A battery level monitor with I²C interface, used to provide the State of Charge (SOC) estimation for the battery.
- SD Card Module: Provides local data storage, communicating with the ESP32 using the SPI protocol for faster read/write operations.
- E-Ink Display: A low-power e-paper display with an SPI interface for minimal energy consumption. It includes the following control signals: EPD_CS, EPD_DC, EPD_RST, and EPD_BUSY.
- W25Q512JVEIQ (64MB NOR Flash): External flash memory connected via SPI, used for storing firmware or large datasets.
- BOOT and RESET Buttons: Connected to GPIO pins to manage the bootloader activation and system reset.
- MCP73831: A Li-Po battery charging controller, responsible for managing the charging process of the battery.
- XC6220A331MR-G (LDO Regulator): A 3.3V voltage regulator that powers the logic circuits of the system from the battery or USB input.
- USB-C Port (USB4110-GF-A): Provides power input and serves as the serial interface for code uploading and debugging.

## Pins description:
- IO0 - INT_RTC: Interrupt signal from the RTC that can wake up the ESP32 from deep sleep. This pin is used by the RTC.
- IO1 – 32KHZ: The 32.768 kHz clock output from the DS3231 RTC, routed to the ESP32 for accurate timekeeping.
- IO2 – MISO: This is the Master In Slave Out pin for SPI communication, used for NOR Flash, E-Paper, and microSD data transfer.
- IO3 - EPD_BUSY: E-Ink Display status signal that indicates whether the screen is busy. The ESP32 reads this to determine when it can send the next display update.
- IO4 – SS_SD: SPI Select pin for the microSD card, ensuring it does not conflict with other SPI devices using Chip Select (CS) lines.
- IO5 – EPD_DC: E-Ink Display Data/Command line used to differentiate between command and data states.
- IO6 – SCK: The SPI Clock pin, used to synchronize data transmission for peripherals like NOR Flash, E-Paper, and microSD.
- IO7 – MOSI: Master Out Slave In pin for SPI communication, used to send data to NOR Flash, E-Paper, and microSD.
- IO9 – IO/BOOT: This is a GPIO pin used for entering programming mode and activating the bootloader when the system is powered on.
- IO10 - EPD_CS: E-Ink Display Chip Select pin, allowing the display to be selected during SPI communication without interfering with other devices.
- IO11 – FLASH_CS: Chip Select pin for the NOR Flash memory, used to activate the flash memory module during SPI communication.
- IO12 – USB_D-: USB Data- line, directly connected to the USB-C connector, enabling power input and data transfer for code uploading and debugging.
- IO13 – USB_D+: USB Data+ line, also routed to the USB-C connector, enabling data transfer for serial communication and debugging.
- IO15 – IO/CHANGE: A GPIO pin used for user-defined actions, such as navigating between pages or changing modes.
- IO16 – TX: Serial Transmit pin used for flashing the older ESP chips and for serial debug logs.
- IO17 – RX: Serial Receive pin used for receiving data during flashing and for serial communication in debug mode.
- IO18 – RTC_RST: Manual Reset pin for the RTC module. It can be used to reset the RTC for synchronization or during a watchdog reset.
- IO19 – I2C_PW: Provides 3.3V to power I²C peripherals, including the RTC, BME688, and battery gauge modules.
- IO20 – EPD_3V3_C: A 3.3V supply line dedicated to powering the E-Ink Display.
- IO21 – SDA: I2C Data line used for communication with the RTC, BME688, and other I²C devices.
- IO22 – SCL: I2C Clock line used for synchronization of data transfer between the ESP32 and I²C devices.
- IO23 – EPD_RST: E-Ink Display Reset pin used to initialize the display before any updates or during power-up.

## Power Consumption:
The system is designed to operate efficiently, with attention to low power consumption. The E-Ink Display is a key contributor to low energy use, as it only requires power during updates. The ESP32-C6 is capable of entering deep sleep modes, significantly reducing power consumption when the system is idle. Additionally, the MAX17048 battery level monitor and the MCP73831 charging controller help in managing the battery's state of charge and ensuring efficient power use throughout the device's operation.

By using SPI for fast data communication with peripherals and I²C for sensors, the system ensures high-performance data transfer while minimizing the number of active pins, which helps in keeping the overall power usage low.
