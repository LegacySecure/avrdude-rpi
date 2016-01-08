Using avrdude with the Raspberry Pi
===================================

Based on [mharizanov's](https://github.com/mharizanov/avrdude-rpi) fork of [deanmao's](https://github.com/deanmao/avrdude-rpi) original work.

Since the Raspberry Pi lacks a DTR pin that makes it oh-so-easy to upload your hex files into
the avr, we need this hack to make it just as easy.  When you wire up your atmega chip, be sure
to connect one of the digital gpio pins to the reset pin, and then you'll be able to use avrdude
as if your serial cable actually had a dtr pin.

Instructions:
-------------

Install using script:

    $ git clone https://github.com/LowPowerLab/avrdude-rpi ~/avrdude-rpi && ~/avrdude-rpi/install

Manual Install: 

Copy both files into your /usr/bin directory, then rename the original avrdude to avrdude-original
and symlink avrdude-autoreset to become avrdude.

    cp autoreset /usr/bin
    cp avrdude-autoreset /usr/bin
    mv /usr/bin/avrdude /usr/bin/avrdude-original
    ln -s /usr/bin/avrdude-autoreset /usr/bin/avrdude

Modify the autoreset script to use the pin that you wired up to the reset pin.  See the line in
autoreset where we do "pin = 22" and change the 22 to your gpio pin number.

Now when you run avrdude from anywhere (including via arduino's normal UI) it will flag dtr when
it is about to upload hex data.

http://www.deanmao.com/2012/08/12/fixing-the-dtr-pin/

Make sure Python is installed
$sudo apt-get update
$sudo apt-get install python-dev
$sudo apt-get install python-rpi.gpio
