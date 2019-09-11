# Serial pressure logging for Agilent ion pump controllers

This is a simple script that communicates with an Agilent ion pump controller over a
serial connection and logs the pressure to a text file.

The script is configured to log channels 1 and 2, and assumes the ion pump controller is
connected via a USB to serial adapter on on /dev/ttyUSB0.

There is no configuration, if you want to log different channels or us a different
serial port, manually modify the script to do so.

This code is Python 2 and Python 3 compatible, requires the `pyserial` library, and has
been tested on a raspberry pi. To access the serial port you may need to configure
permissions to allow the user to read /dev/ttyUSB0, or you may simply run this script
with sudo/as root.

The script should in principle work on Windows if you modify /dev/ttyUSB0 to 'COM1' or
similar, but I have not been able to communicate with an Agilent ion pump controller
from Windows 7 over USB to serial at all - with this script or otherwise - despite the
same USB to serial adapter working with other serial devices. Your mileage may vary.

I do not intend to develop this code further, the main purpose of publishing it is to
document for myself and others the packet format for communicating with the ion pump
controller. Although documented in the ion pump controller manual, when implementing
this script, we wasted time before realising that the hex characters to be sent as ascii
for the checksum of each packet needed to be *upper case*, as this was not specified in
the documentation (and does not apply for digits 0-9 and so was only intermittently a
problem and hence hard to debug).