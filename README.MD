# AD57X4/R Arduino Library
This library is based on [janelia-arduino/AD57X4R: Provides an SPI based interface to the AD5724R, AD5734R, and the AD5754R Quad 12-/14-/16-Bit Unipolar/Bipolar Voltage Output DACs.](https://github.com/janelia-arduino/AD57X4R/tree/main).

The library has been updated to explicity enable the internal reference, making this compatible with non-R versions (ie, AD57X4), as well as the ability to specify the SPI clock speed.

**Changelog**
- Hardcoded SPI_BIT_ORDER and SPI_MODE after encountering data type issues
- Protected digitalWrite() is chip select is not initialized
- Option to set externalRef at construction; 0 (default) indicates use of internal reference that will set `vref_` to 2.5V
- With new use of `vref_`, getVoltageMin() and getVoltageMax() were updated

## Description

Provides an SPI-based interface to the AD5724R, AD5734R, and AD5754R Quad 12-/14-/16-Bit Unipolar/Bipolar Voltage Output DACs.

See [AD5724R/AD5734R/AD5754R (Rev. G)](https://www.analog.com/media/en/technical-documentation/data-sheets/AD5724R_5734R_5754R.pdf).

The outputs can be set in two ways:

1. Setting the Analog Value
The analog values are integers, with the range determined by the resolution and whether the output is set to unipolar or bipolar. This method is similar to Arduino’s analogWrite and is provided under that name for convenience.

2. Setting the Voltage Directly
Output voltages can also be set directly as floats, with the minimum and maximum values determined by the output range.

By default, the outputs are updated immediately after they are set. However, they can also be updated synchronously using the simultaneous update methods.

### Wiring

| PIN       | CONNECTION                                                                    |
|-----------|-------------------------------------------------------------------------------|
| SDIN      | connect to processor MOSI pin or SDO of previous daisy-chained chip           |
| SDO       | connect to processor MISO pin or SDIN of next daisy-chained chip              |
| SCLK      | connect to processor SCK pin                                                  |
| SYNC      | connect to processor CS pin and set in constructor or setChipSelectPin method |
| BIN2SCOMP | GND                                                                           |
| LDAC      | GND or connect to processor pin and use setLoadDacPin method                  |
| CLR       | DVCC or connect to processor pin and use setClearPin method                   |
