A Journey to Raspberry Pi
---

Existing Audio Gears  
DAC Upgrade for sound quality and DSD support  
Asus RT-AC66U not recognize SMSL M8 - Switch to Windows  
Switch to low watt MPD with SMSL M8 support  
Add video player on another SD card  
Unify to a single SD card dual boot  
Customizing for easy switch between Rune and OSMC  
Customizing for consistency and easier switch and control  
Add remote control for power on/off in sequence  
Unify Remote Control  
Final System Setup  
Transfer from SD card to USB drive  
Tweaks  

**Existing Audio Gears**  

	- Files		USB hdd (on Asus RT-AC68U router)  
	- Syste		TomatoUSB on Asus RT-AC68U router  
	- Software	MPD  
	- DAC		built-in USB (Musical Fidelity A1)  
	- Amplifier	Musical Fidelity A1 Integrated Amplifier  
	- Speakers	Focal Aria 926, Falcon LS3/5a  
	- Subwoofer	Acoustech PL-200  
	
**DAC Upgrade for sound quality and DSD support**  

	- DAC		SMSL M8 ES9018K2M 24Bit/384KHz (XMOS USB, coax, optical)  
	
**Asus RT-AC66U not recognize SMSL M8 - Switch to Windows**  

	- Files		Samba shares from Asus RT-AC66U router  
	- System	Windows 10 laptop  
	- Software	JRiver  
	
**Switch to low watt MPD with SMSL M8 support**  

	- System	Raspberry Pi 3  
	- Distro	RuneAudio  

	MPD based Distros:  
		Moode  
			hard to reach bit perfect output  
		Rune  
			bit perfect ready  
			DSD ready  
			very satisfying result  
		Volumio  
			satisfied with Rune  
			no chance to try yet  
			
**Add video player (on another SD card)**  

	- Distro	OSMC  
	- Display	LG 55LM7600  
	
	Kodi based Distros:  
		- OpenELEC  
			limited customizable  
		- OSMC  
			satisfying result with some other great skins  
			
**Unify to a single SD card dual boot**  

	- Software	NOOBS
	
	Multi Boot:  
		- BerryBoot  
			can install directly to USB drive  
			support HDMI CEC  
			squashfs filesystem needs some skills and patient  
			Rune outputs loud static noise with some USB DAC  
		- NOOBS  
			manageable customizing  
			filesystem can be extracted directly from image file  
		
**Customizing for easy switch between Rune and OSMC**  

	- Device	Mouse with modified on-screen UI  
	
**Customizing for consistency and easier switch and control**  

	- Device	USB PC remote (dirt cheap on eBay)  
	
	Remote Control:  
		- HDMI CEC - OSMC only  
			need no additional device but the TV must support CEC  
			cannot control NOOBS  
			automatic switch input hassles  
		- ir module - NOOBS + OSMC  
			can receive any signal but a lot of key code detection  
			need a lot of keymaps  
			cannot control NOOBS  
			cheap but need DIY enclosure  
		- ir USB PC Remote - NOOBS + Rune + OSMC  
			recognized as a keyboard and mouse  
			control NOOBS boot menu  
			work in Rune with a single config file  
			ready to use without settings in OSMC  
			cheap and easy to install to USB  
		
	Configuration:  
		- Rune  
			not directly support keyboard  
			use XbindKeys to map keyboard key to command  
			detect ir code  
		- OSMC  
			directly support keyboard  
			detect ir code with Keymap Editor addon  
			create /home/osmc/.kodi/userdata/keymaps/keyboard.xml  
			restart keymaps  
			map 'reloadkeymaps' command to a key  
			add /home/osmc/bootrune.py  
	
**Add remote control for power on/off in sequence**  

	- Device	Relay module control by GPIO (dirt cheap on eBay)  
	
	Remote Control  
		- AC power:  
			switch on/off amp, pre-amp, DAC in sequence  
			autoswitch off on idle  
			autoswitch off on shutdown  
		
	RPi.GPIO  
		- Rune  
			edit 'sudoers' to allow no-password sudo  
			use php sudo to call python script that cannot sudo by itself  
			use 'python-mod2' to monitor idle  
			use python 'requests' for pushstream notification  
			use pushstream message for GPIO button updating  

		- OSMC
			('sudoers' already no password)
			use python sudo to call python script that cannot sudo by itself
			use python 'requests' for json-rpc
				monitor idle
				notification
	
**Unify Remote Control**  

	- Devices	JP1 remote (universal programmable)  
			JP1 FTDI USB to serial cable  
	- Software	RemoteMaster  
	
	- JP1 Remote	learn any remotes  
			most remotes code available for download  
			discrete on, discrete off, discrete input  
			map any signals to any keys  
			macro signals  
		
**Final System Setup**  
	- Raspberry Pi 3  
	- [Dual Boot (NOOBS) - Rune | OSMC](https://github.com/rern/RPi2-3.Dual.Boot-Rune.OSMC)  
	- [Remote](https://github.com/rern/Rune_USB_PC_Remote)  
	- [GPIO](https://github.com/rern/RuneUI_GPIO)  
	- [JP1 Remote](http://www.hifi-remote.com/)  
				
**Transfer from SD card to USB drive**  

	- transfer static files  
	- set boot partition in /boot/cmdline.txt  
			
**Tweaks**  

	- Make installation unattended  
		append silentinstall to cmdline.txt  
		custom compile NOOBS to auto reboot on finished  
		
	- Auto switch audio output to USB  
		Rune  
			replace mpd.conf with on.py  
		OSMC  
			get udev parameters  
			create udev rules  
	- Change OSMC root ssh login to be the same as Rune  

	- Modify on-screen user interface  
		Rune  
			add 'amp' on/off button  
			add 'bootosmc' menu  
		OSMC  
			add 'amp' on/off menu  
			add 'bootrune' menu  
