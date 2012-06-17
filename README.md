lamma500
========

Lamma 500 Dragonboat Festival - WiFi setup

Jon Buford asked me to help out with connectivity during the
Lamma 500 Dragonboat Festival on May 6, 2012

There was an initial phone call with Malcolm Morris of the organization team on April 8, four weeks before the event. I joined two meetings before the event with the organization team, the last one before the event on May 2.

The requirements were defined as follows:

3 Locations, "beach" with Internet uplink, "start" and "finish" line

There is no direct line of sight between "start" and "finish", the distance between these two is 500m. Both "start" and "finish" have line of sight to "beach", so we decided to use "beach" as the hub and uplink point to the Internet.

Stable Internet connectivity is required for sharing files with dropbox. Dropbox can sync files via the LAN, but this still requires Internet connectivity.

We decided to install two Ubiquiti Airgrid M5 at the beach, one Airgrid M5 at the start line, and an Ubiquiti NanoStation M5 at the finih line. The "beach" endpoints would be configured as APs, "start" and "finish" as STA (client).

Each location would get a TP-Link WR1043ND for local WiFi access.

Internet connectivity would be provided using a TP-Link MR3020 3G router, connected to the WAN port of the "beach" WR1043ND.
 
Network setup for Lamma 500 2012

Device 1 (beach)

TP-Link WR1043ND

Install stable OpenWRT backfire 10.03.1 from
http://downloads.openwrt.org/backfire/10.03.1/ar71xx/openwrt-ar71xx-tl-wr1043nd-v1-squashfs-factory.bin

Log in as root, set root password

Install packages:

opkg install kmod-usb-acm kmod-usb-core kmod-usb-ohci kmod-usb-s
erial kmod-usb-serial-option kmod-usb-uhci kmod-usb2 usb-modeswitch usb-modeswit
ch-data usbutils ppp ppp-mod-pppoe chat comgt

Add the following to /etc/config/network:

Code:
config 'interface' 'wan3g' 
        option 'ifname' 'ppp0' 
        option 'apn' 'csl3p' 
        option 'service' 'umts' 
        option 'proto' '3g' 
        option 'device' '/dev/ttyUSB2'

Connect 3G stick with CSL SIM card.

Make sure USB Modeswitch works with D-Link DWM-156

http://www.draisberghof.de/usb_modeswitch/bb/viewtopic.php?t=817

IP address (LAN): 192.168.6.1

Network Camera

LevelOne WCS-0010 HW Ver. 2.0
Manual:

http://download.level1.com/level1/manual/FCS-0010_WCS-0010_UM_V2.1.pdf
IP: 192.168.6.123
Multicast IP: 224.2.0.1
5GHz devices

Host finish-beach
Ubiquiti Nanostation 5 loco
Wireless mode: STA
ESSID finish-beach.lamma500.com
IP: 192.168.6.112
login: root/relax11
Security: WPA2-PSK AES, PSK: l@mm@500-2012

Host beach-finish
Color code: RED
Ubiquiti Airgrid M5 11”x17”
Airgrid M5-HP 11x14”
MAC: 00:27:22:5a:25:56
IP: 192.168.6.111
Login: root/relax11
Wireless mode: AP
ESSID finish-beach.lamma500.com
Frequency: Channel 149 (5745 MHz)
Security: WPA2-PSK AES, PSK: l@mm@500-2012

Host beach-start
Color code: BLACK
Ubiquiti Airgrid M5 17”x24”
WLAN0 MAC00:27:22:5A:24:FF
LAN0 MAC00:27:22:5B:24:FF
IP: 192.168.6.101
Login: root/relax11
Wireless mode: AP
ESSID finish-start.lamma500.com
Frequency: Channel 165 (5825 MHz)
Security: WPA2-PSK AES, PSK: l@mm@500-2012

Host start-beach
Color code: WHITE
Ubiquiti Airgrid M5 17”x24”
WLAN0 MAC 
LAN0 MAC 00:27:22:56:f4:7e
IP: 192.168.6.102
Login: root/relax11
Wireless mode: STA
ESSID finish-start.lamma500.com
Frequency: Channel 165 (5825 MHz)
Security: WPA2-PSK AES, PSK: l@mm@500-2012

