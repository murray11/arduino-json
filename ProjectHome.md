This small library allows developers to remotely read and write data from <a href='http://www.arduino.cc/'>Arduino</a> projects using simple HTTP requests and JSON responses.  Built to work with the <a href='http://asynclabs.com/'>AsyncLabs WiShield</a>. This library listens on port 8181 for a command and up to 2 arguments.  It generates and sends a JSON response.

## Currently supported commands ##
  * write\_eeprom( int loc, int value )
  * write\_dpin( int pin, int val )
  * write\_shared( int loc, int value )
  * read\_eeprom ( int start, int finish )
  * read\_dpin( int pin )
  * read\_adpin( int pin )
  * read\_shared()

**"shared"** is a public array of 16 unsigned integers, accessed through the RemoteJSON class. It should be used to avoid unnecessary reading/writing EEPROM to communicate with the device.

## Request Format ##
Requests are made in the following format:
> GET /`<command>`/`<arg1>`/`<arg2>`/

## Example Usage ##
To read EEPROM from location 0 to 5 from a device at 10.0.0.1, simply make an HTTP request to `http://10.0.0.1:8181/read_eeprom/0/5/`

The JSON response would be:
`{"result":[0,0,0,0,0]`}

## Status and TODO ##
This project is still in early development. Still some things todo:
  * Java Client Library: develop a java library for easily communicating with the device. For example, calls should be as easy as `RemoteArduino.readAnalog(PIN1)`, etc.
  * Support for custom commands: add support to let developers easily supply custom commands and response for those commands.
  * Add support for responses longer than 444 bytes