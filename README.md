*** IMPORTANT ***

Please note this repository is deprecated, and the code is not up-to-date to use on The Things Network.

This repository will not be further maintained. Please find another repository if you want to deploy a single channel gateway.


Single Channel LoRaWAN Gateway
==============================
This repository contains a proof-of-concept implementation of a single
channel LoRaWAN gateway.

It has been tested on the Orange Pi Zero 512MB platform (OS ARMBIAN 5.35 Debian GNU/Linux 8 (jessie) 3.4.113-sun8i), using a Semtech SX1278 transceiver (RA-02 module)

The code is for testing and development purposes only, and is not meant 
for production usage. 

Part of the source has been copied from the Semtech Packet Forwarder 
(with permission).

Features
--------
- listen on configurable frequency and spreading factor
- SF7 to SF12
- status updates
- can forward to two servers

Not (yet) supported:
- PACKET_PUSH_ACK processing
- SF7BW250 modulation
- FSK modulation
- downstream messages (tx)

Dependencies
------------
1. SPI needs to be enabled on the Orange Pi Zero
  Please, check this - run command 
 
 - ls -l /dev/spidev*
 
 and see result:
 
-crw------- 1 root root 153, 0 Jan 11 16:31 /dev/spidev0.0
-crw------- 1 root root 153, 1 Jan 11 16:31 /dev/spidev1.0
 
 If you see in list line /dev/spidev1.0 - all OK

2. You need install my modified library WiringOP-Zero

-git clone https://github.com/vladikoms/WiringOP-Zero.git
-cd WiringOP-Zero
-chmod +x ./build
-sudo ./build

3. Run packet forwarder as root

Connections
-----------
-SX1278 - Orange Pi Zero

- 3.3V   - 3.3V (header pin #1) 
- GND	   - GND (pin #25)
- NSS    - GPIO6 (pin #7)
- DIO0   - GPIO7 (pin #12)
- RST    - GPIO0 (pin #13)
- MOSI   - MOSI (pin #19)
- MISO   - MISO (pin #21)
- SCK    - CLK (pin #23)

Configuration
-------------

Defaults:

- LoRa:   SF7 at 433.9 Mhz
- Server: 54.229.214.112, port 1700  (The Things Network: croft.thethings.girovito.nl)

Edit source node (main.cpp) to change configuration (look for: "Configure these values!").

Please set location, email and description.

Installing
----------

git clone https://github.com/vladikoms/single_chan_pkt_fwd.git
cd single_chan_pkt_fwd
make

Run
---

sudo ./single_chan_pkt_fwd

License
-------
The source files in this repository are made available under the Eclipse
Public License v1.0, except for the base64 implementation, that has been
copied from the Semtech Packet Forwader.

