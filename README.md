# LoRa_BLE_Sensor Board
CAD: KiCad 9.0
# Overview
A RAK4630 based sensor board that uses BLE and LoRaWAN. This board is configured to use two industrial sensors and a relay simultaneously. 
It is designed so the sensor can be powered with 3.3V, 5V, 12V or 24V that are switched between through firmware. It is designed for each sensor to have its own unique 
power supply, independent of the other sensor. It is designed for work with either digital or analog sensors. 

# Schematic Breakdown
**RAK4630** 
 - A combination module of an nRF52840 and SX1262
   * The nRF52840 has a cortex M4 and uses BLE
   * The SX1262 is a SPI controlled LoRa chip
 - There is an SWD connector for programming
 - There are two buttons
   * SW1 is connected to the reset pin on the nRF52840
   * SW2 is connected to P0.09

**NPM1300** 
 - Power management for the board
   * Programmable over I2C with the RAK4630
 - Used to charge the battery and works as a fuel guage
 - Contains two buck converters
   * Buck 1 is used to power the 3V relay
   * Buck 2 is used at 3.3V to supply Vdd for the entire board
 - Contains 2 LDOs
   * Used if either sensor is set to 3.3V
 - Switch SW3
   * Used to change power modes on npm1300 or to do a power cycle of the board
 - RGB LED
   * Used for charging/error status of the npm1300 and as an led controlled by RAK4630

**Boost 1** 
 - TLV61046ADBVR Boost Converter
   * Up to 28V output with load disconnect
   * Output is determined by resistors in feedback
 - NMOS mosfets
   * Allow for feedback reistances to be changes to adjust output
   * BOOST1_FB_CTRL1 set to 0, BOOST1_FB_CTRL2 set to 0 --> 24V
   * BOOST1_FB_CTRL1 set to 1, BOOST1_FB_CTRL2 set to 0 --> 12V
   * BOOST1_FB_CTRL1 set to 0, BOOST1_FB_CTRL2 set to 1 --> 6V
   * BOOST1_FB_CTRL1 set to 1, BOOST1_FB_CTRL2 set to 1 --> 5V

**Boost 2** 
 - TLV61046ADBVR Boost Converter
   * Up to 28V output with load disconnect
   * Output is determined by resistors in feedback
 - NMOS mosfets
   * Allow for feedback reistances to be changes to adjust output
   * BOOST2_FB_CTRL1 set to 0, BOOST2_FB_CTRL2 set to 0 --> 24V
   * BOOST2_FB_CTRL1 set to 1, BOOST2_FB_CTRL2 set to 0 --> 12V
   * BOOST2_FB_CTRL1 set to 0, BOOST2_FB_CTRL2 set to 1 --> 6V
   * BOOST2_FB_CTRL1 set to 1, BOOST2_FB_CTRL2 set to 1 --> 5V

**Power Switches** 
 - Connects boost and ldo outputs so only 1 is used by the sensor
   * Boost outputs have priority if both are enabled
 - ESD protection for sensor power
   * Designed for 24V
   
**Digital Inputs** 
 - MOSFET based level shifters
   * Allows sensor digital logic to be translated from sensor power to Vdd
 - ESD protection for digital inputs
   * Designed for 24V

**Analog Inputs** 
 - 4 inputs meant for external sensors
   * 2 designed for 4-20mA current sensors
   * 2 designed to read voltages up to 28V
   * 2 designed for feedback to the voltage of the sensor power

**Relay** 
 - Designed for 3V DPST relay that has a activation current below 200mA

**USB** 
 - 6 pin jst PH connector to use with external USB-C connector
 - ESD protection for data lines and USB power

**Interface** 
 - Two screw terminal connectors for the sensors
   * Designed for pluggaple screw terminals
 - One 2.54mm pin header for debugging 

# Power Analysis

# Bugs/To-Do

# Revision History
Current Version: **V1.0**

Version Breakdown: `[Major Chanegs]`.`[Minor Changes]`

### V1.0
- Initial Design of Board
