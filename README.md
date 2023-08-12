# MT7688-OpenOCD
OpenOCD configuration for MT7688AN/MT7688KN/MT7628x

# How to do it  
OpenOCD configuration file for MT7688AN/MT7688KN/MT7628x.  
Please believe that he can revive a completely bricked router/smart device/various IoT devices, even your device flash has been completely damaged/blank/unsoldered.  
The code has passed the test on MT7688AN, the test equipment is OrangePi, using bitbang (that is, gpio software simulation) to communicate with MT7688AN.  
Theoretically common to all MT76x8 series soc.  

# How to use
MT76X8 series are SoC chips with MIPS-24kec core. This series of SoC provides JTAG interface for debugging. For MT7688 series, the relevant pin definition and operation process are as follows:  
When using it, you only need to start the SoC in DBG_JTAG_MODE mode. To enter this mode, you only need to pull the UART_TXD1 (No. 111) pin to a low level to power on.
In this mode, the 5 Ethernet status LEDs correspond to the following:  
143 EPHY_LED0 JTDO  
142 EPHY_LED1 JTDI  
141 EPHY_LED2 JTMS  
140 EPHY_LED3 JTCLK  
139 EPHY_LED4 JTRST_N  

If you need a reset signal, it can be drawn on the following pins:  
138 PORST_N  

# How to use  
Download debug.cfg and ramboot.bin, where debug.cfg is the OpenOCD configuration file, ramboot.bin is the pre-compiled uboot, and the code space is located in the memory.
Please start OpenOCD with this configuration file:  
openocd -f /path/to/debug.cfg  
After that, please telnet to connect to the openocd session, and execute the ddrinit command to initialize the DDR memory.  
After the DDR memory is initialized successfully, execute the load_ramboot command to download uboot to ram and run it. After that, you can use uboot to burn new codes to flash.  

# Special Instructions  
You can also compile your own uboot and use this script to download to ram to run, of course, you need to find a way to compile uboot to MT76x8 by yourself.  
This project can automatically identify your DDR and soc type, theoretically it can be used for all MT76x8 series chips.  
If ramboot.bin is loaded successfully but there is still no output from the serial port, it may be that your device does not have any firmware at all. In this case, you can try to use ramboot-cache.bin instead of ramboot.bin to load into the device.  


