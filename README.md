# wiiclassic-kbd
Use wii classic controller via I2C as a virtual keyboard.

Original source for most of the code is the program nunchuk.c from "Mastering the Raspberry Pi" - ISBN13: 978-1-484201-82-4 by Warren Gay

Modified to use the Wii Classic Controller, over an I2C connection on a Raspberry Pi 3. This was based on documentation of the I2C data frame used by the controller published by wiibrew.org. As a source of inspiration for this project, Adafruit's Retrogame project showed that the GPIO based inputs could be pushed as keyboard inputs using uinput/evdev. Instead of using GPIO, this project uses I2C, but the keyboard functionality is the same.

The program uses linux/uinput.h to allow the classic controller to be used as a virtual keyboard. Seems to work just fine as is with RetroPie.

Current functionality: buttons emulate keyboard key press / releases. The analog joysticks can be read, but are currently unused.

With RPi:
- run raspi-config, select Advanced, enable I2C.
- install libi2c-dev and i2c-tools packages

`gcc -o classic classic.c`
`mv classic /usr/local/bin`
`chmod 755 /usr/local/bin/classic`

`sed -i "s/^exit 0/\/usr\/local\/bin\/classic \&\\nexit 0/g" /etc/rc.local >/dev/null`

