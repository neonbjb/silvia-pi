# cremina-pi
An application that runs on the Raspberry Pi which allows users to monitor brew variables for the Olympia
Express Cremina espresso machine.

#### Currently Implemented Features:
* One temperature input from a MAX6675 thermocouple. (Intended to be fastened to the group)
* Load cell measurement capacity so lever pressure can be converted to brew pressure.
* RESTful API
* Web interface for displaying temperature and other statistics

#### Dashboard
<img src="https://github.com/brycesub/cremina-pi/blob/master/media/silvia_dashboard.gif" width=800 />

#### Hardware
* Raspberry Pi 2
  * $35 - http://www.amazon.com/Raspberry-Pi-Model-Project-Board/dp/B00T2U7R7I
  * $5 - Raspberry Pi Zero should work too
* Wi-Fi Adapter that works with Raspbian
  * $10 - http://www.amazon.com/Edimax-EW-7811Un-150Mbps-Raspberry-Supports/dp/B003MTTJOY or
  * $10 - http://www.amazon.com/Tenda-150Mbps-Wireless-Adapter-W311MI/dp/B006GCYAOI
* Power Adapter
  * Any Micro USB 5v / 2A supply will do, the longer the cable the better
  * $9 - http://www.amazon.com/CanaKit-Raspberry-Supply-Adapter-Charger/dp/B00GF9T3I0
* Micro SD Card
  * 4GB minimum, 8GB Class 10 recommended
  * $7 - http://www.amazon.com/Samsung-Class-Adapter-MB-MP16DA-AM/dp/B00IVPU7KE
* Solid State Relay - For switching on and off the heating element
  * $10 - https://www.sparkfun.com/products/13015
* Thermocouple Amplifier - For interfacing between the Raspberry Pi and Thermocouple temperature probe
  * $15 - https://www.sparkfun.com/products/13266
  * MAX6675 Thermocouple amps can be supported, but you will need to modify the Adafruit31855 library.
* Type K Thermocouple - For accurate temperature measurement
  * $15 - http://www.auberins.com/index.php?main_page=product_info&cPath=20_3&products_id=307
* Ribbon Cable - For connecting everything together
  * $7 - http://www.amazon.com/Veewon-Flexible-Multicolored-Female-Breadboard/dp/B00N7XX4XM
    * Female to Female if using the Raspberry Pi 2
  * $5 - http://www.amazon.com/uxcell-Width-Colorful-Flexible-Ribbon/dp/B00BWFY6JI
    * Bare wire if using the Raspberry Pi Zero
* 14 gauge wire - For connecting the A/C side of the relay to the circuit
  * $5 - Hardware Store / Scrap
    * Don't skimp here.  Remember this wire will be in close proximit to a ~240*F boiler

#### Hardware Installation
[Installation Instructions / Pictures](http://imgur.com/a/3WLVt)

#### Circuit Diagram
High-level circuit diagram:

![Circuit Diagram](media/circuit.png?raw=true "Circuit Diagram")

NOTE: This custom version of cremina-pi requires that you connect the SSR in reverse!
e.g. Connect the Raspberry Pi 5V line to the SSR (+) and pin BCM7 to SSR (-).

#### Software
* OS - Raspbian Jessie
  * Full - https://downloads.raspberrypi.org/raspbian_latest
  * Lite (for smaller SD Cards) - https://downloads.raspberrypi.org/raspbian_lite_latest

Install Raspbian and configure Wi-Fi and timezone.

#### cremina-pi Software Installation Instructions
Execute on the pi bash shell:
````
sudo apt-get -y update
sudo apt-get -y upgrade
sudo apt-get -y install rpi-update git build-essential python-dev python-smbus python-pip
sudo rpi-update
sudo bash -c 'echo "dtparam=spi=on" >> /boot/config.txt'
sudo reboot
````

After the reboot:
````
sudo git clone https://github.com/brycesub/cremina-pi.git /root/cremina-pi
sudo /root/cremina-pi/setup.sh
````
This last step will download the necessary python libraries and install the cremina-pi software in /root/cremina-pi

It also creates an entry in /etc/rc.local to start the software on every boot.
