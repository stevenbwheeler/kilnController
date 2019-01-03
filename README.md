kilnController
==============

Turns a Raspberry Pi into a cheap, universal & web-enabled kiln Controller.
Forked from the reflow oven project: [picoReflow](https://apollo.open-resource.org/mission:resources:picoreflow) which I found through a blog post on [succulent ceramics](http://succulentceramics.com/2016/10/07/wifiraspberry-kiln-controller/)

I used this to add a firing schedule control to a little pottery kiln I picked up second hand. The kiln is 10A/240V rated to 1000 degrees C. It had a door switch and a basic thermostat which allowed for 25%, 50%, 75% or 100% power but no timer. With the kilnController I can now set it up for a bisque or low temerature glaze firing and leave it to its own devices, checking progress every now and then on my mobile phone or PC. 

**Standard Interface**

![Image](https://apollo.open-resource.org/_media/mission:resources:picoreflow_webinterface.jpg)

**Curve Editor**

![Image](https://apollo.open-resource.org/_media/mission:resources:picoreflow_webinterface_edit.jpg)

## Hardware

  * [Raspberry Pi Zero W](https://raspberry.piaustralia.com.au/raspberry-pi-zero-w) - any pi will do but these are about $15 here in Australia
  * [MAX 31855](https://www.adafruit.com/product/269) Cold-Junction K-Type Thermocouple (about $6 on eBay)
  * [K-Type Thermocouple Sensor](https://www.google.com/search?q=K-Type+Thermocouple+Sensor+1250+1M+SY+site%3Aebay.com.au) -100°C to 1250°C ($3 on eBay)
  * Solid State Relay Module [SSR-25DA](https://www.google.com/search?q=Solid+State+Relay+Module+SSR-25DA+25A+%2F250V+3-32V+DC+Input+24-380VAC+Output+pOK) 25A /250V 3-32V DC Input 24-380VAC Output (again, about $6 on eBay)

## Installation

### Dependencies

We've tried to keep external dependencies to a minimum to make it easily
deployable on any flavor of open-source operating system. If you deploy it
successfully on any other OS, please update this:

#### Currently tested versions

  * greenlet-0.4.2
  * bottle-0.12.4
  * gevent-1.0
  * gevent-websocket-0.9.3

#### Ubuntu/Raspbian

    $ sudo apt-get install python-pip python-dev libevent-dev
    $ sudo pip install ez-setup
    $ sudo pip install greenlet bottle gevent gevent-websocket

#### Gentoo

    $ emerge -av dev-libs/libevent dev-python/pip
    $ pip install ez-setup
    $ pip install greenlet bottle gevent gevent-websocket

#### Raspberry PI deployment

If you want to deploy the code on a PI for production:

    $ pip install RPi.GPIO

This **only applies to non-Raspbian installations**, since Raspbian ships
RPi.GPIO with the default installation.

If you also want to use the in-kernel SPI drivers with a MAX31855 sensor:

    $ sudo pip install Adafruit-MAX31855

### Clone repo

    $ git clone https://github.com/botheredbybees/kilnController.git
    $ cd kilnController

## Configuration

All parameters are defined in config.py, just copy the example and review/change to your mind's content.

    $ cp config.py.EXAMPLE config.py

## Usage

### Server Startup

    $ ./kilncontrollerd.py

### Autostart Server onBoot
If you want the server to autostart on boot, run:

    sudo nano /etc/rc.local

add the line:

    `sudo python /home/pi/kilnController/kilncontrollerd.py &`

### Client Access

Open Browser and goto http://127.0.0.1:8080 (for local development) or the IP
of your PI and the port defined in config.py (default 8080).

## License

This program is free software: you can redistribute it and/or modify
it under the terms of the GNU General Public License as published by
the Free Software Foundation, either version 3 of the License, or
(at your option) any later version.

This program is distributed in the hope that it will be useful,
but WITHOUT ANY WARRANTY; without even the implied warranty of
MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the
GNU General Public License for more details.

You should have received a copy of the GNU General Public License
along with this program.  If not, see <http://www.gnu.org/licenses/>.

## picoReflow

For more info on the parent project, see picoReflow: https://apollo.open-resource.org/mission:resources:picoreflow
