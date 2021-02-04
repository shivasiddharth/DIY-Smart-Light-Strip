# DIY-Smart-Light-Strip
 Its hard to combine both Amazon Alexa and Google Assistant control for a DIY project and that too for free. Thanks to Supla, who have both a Google Assistant app and an Amazon Alexa skill, it was feasible to add smartness to an otherwise dumb light strip.

## Components and Tools
1. Terminal Blocks http://ebay.us/YO7Zha   
2. Wemos D1 Mini http://ebay.us/Tzvi4Q    
3. SMD 5050 RGBWW LED Strip http://ebay.us/APG8W6 or http://ebay.us/4Y0UBK    
4. PCB http://ebay.us/ujStHB     
5. DC-DC Step Down Converter http://ebay.us/EU2Xd5    
6. IRF540N Mosfet http://ebay.us/tiUWHJ      
7. Wires  
8. Solder iron.  
9. Lead free solder wire.   
10. Solder flux.   

## Instructions

### Strip Controller Wiring
![alt text](https://content.instructables.com/ORIG/FG2/T6FQ/KKL5KUUY/FG2T6FQKKL5KUUY.png?auto=webp&frame=1&fit=bounds&md=ac91235a87a63983e98285b2b2b95948)
The smartness to the SMD 5050 strip is added using a NodeMCU/ESP8266 based controller. The strip controller board comprises of:   
1. Wemos D1 Mini/NodeMCU that connects to the internet.   
2. DC-DC converter that steps down the 12V supply to the microcontroller tolerable 5V.   
3. 3 MOSFETS for the Red(R), Green(G) and Blue(B) channels.   
The wiring diagram shows the connection between the different parts.   
A word of caution though. The pins cannot be interchanged and has to be used as it is. The Pins used with Wemos are D6, D7 and D8. They translate to GPIO numbers 12, 13 and 15. Please refer to the pin map attached.    
![alt text](https://content.instructables.com/ORIG/FCF/0BOF/KKL5KV6U/FCF0BOFKKL5KV6U.png?auto=webp&frame=1&fit=bounds&md=1e309afa038c938bdee767ddb11c531e)   

### Preparing a PCB for the Controller   
Populating the components on a PCB makes it more compact and easy on the eyes than having wires dangling between the parts. In the previous step, I had shown the wiring diagram. As the wiring diagram was made in Fritzing, it was easy to design the PCB directly from the wiring diagram.

![alt text](https://content.instructables.com/ORIG/F57/Y9G6/KKL5KVOM/F57Y9G6KKL5KVOM.png?auto=webp&frame=1&fit=bounds&md=51a9342cbe251690e61ba7e48a7d6679)   

As one can probably see, I have mad the supply tracks thick to stand the current draw from the LED Strip. Due to the shortage of time, I soldered the components on a general purpose PCB.

![alt text](https://content.instructables.com/ORIG/FN9/E4A4/KKL5N058/FN9E4A4KKL5N058.jpg?auto=webp&frame=1&crop=3:2&width=624&height=1024&fit=bounds&md=c5bffa0454b5033c388b4d898f3fa920)   

Those who wish may fabricate the PCB using the Fritzing or the Gerber files attached. There are a number of different PCB fabrication providers, but I recommend JLCPCB (https://jlcpcb.com) for fabricating the PCB purely based on my experience.

Link to the Fritzing file: https://mega.nz/file/a0xGFJjT#1llAj0IeAiGFmeHzPdaW...
Link to the Gerber file: https://mega.nz/file/m4gAUDCa#UPfquIzSdDWayZLJ8wdg...

### Prerequisites for the Controller Software/firmware
The Google Assistant and Amazon Alexa integration is quite complex for DIY projects. In this instructable, we will be making use of SUPLA (a free home automation service provider) for their built-in Google Assistant and Amazon Alexa integration.

1. First head over to https://cloud.supla.org/login and login or create an account if you already dont have one. immediately after logging in you will be presented with a screen that looks like the following image.
![alt text](https://content.instructables.com/ORIG/FQN/IOJV/KKL5KXYH/FQNIOJVKKL5KXYH.png?auto=webp&frame=1&width=1024&height=1024&fit=bounds&md=7cf4b07f8d891e31cdfe1e726920e67a)
The credentials under supla-dev will go into the NodeMCU/Wemos and the supla-client credentials will go into the SUPLA phone/tablet app. Leave it opened as we will comeback to it again (Do not share the credentials. I changed my credentials and no longer use the ones shown here).

2. Next, go to https://www.supla.org/en/download webpage and scroll down untill you get to the "H801 WIFI LED CONTROLLER" tab. Click on the download button to download the binaries that needs to be flashed onto the NodemCU/Wemos.
![alt text](https://content.instructables.com/ORIG/FKB/LBDP/KKL5KYW7/FKBLBDPKKL5KYW7.png?auto=webp&frame=1&width=1024&height=1024&fit=bounds&md=67b5767812a6680bc6c8f9ce0092cb2c)
3. Download the FLASH DOWNLOAD TOOLS from the Espressif's downloads page https://www.espressif.com/en/support/download/othe... There seems to be only a Windows version, however you can refer this post for running the flash download tools on a macOS machine https://blog.squix.org/2015/05/esp8266-flashing-no...
![alt text](https://content.instructables.com/ORIG/FNF/QT2I/KKL5KYXA/FNFQT2IKKL5KYXA.png?auto=webp&frame=1&width=1024&height=1024&fit=bounds&md=c0209b9361b1c65b821c5745483adc4a)
4. Unzip both the H801 and Flash Download Tools zip files into separate folders.
Next, we will take a look into the firmware flashing process.

### Flashing the Firmware
1. From the unzipped flash download tool folder, double clikc and run flash_download_tool_x.x.x.exe file.

2. In the first pop-up window choose Developer mode and in the subsequent pop-up window choose ESP8266 DeveloperTools.
![alt text](https://content.instructables.com/ORIG/FX1/NZSN/KKL5KZ68/FX1NZSNKKL5KZ68.png?auto=webp&frame=1&width=1024&fit=bounds&md=27623cfca275d56225ba4fc5fedb809d)    

![alt text](https://content.instructables.com/ORIG/FMJ/HTNI/KKL5KZ67/FMJHTNIKKL5KZ67.png?auto=webp&frame=1&width=1024&fit=bounds&md=8b30d2d0553c3333a38706a68b17cbeb)
3. Now open the Readme file in the unzipped H801 folder. This has the details pertaining to the flashing settings.
4. In the ESP8266 Download Tool window, the left side space is for the path to the binaries and the right side space is for the corresponding flash address.   
![alt text](https://content.instructables.com/ORIG/F7J/TQI3/KKL5KZ66/F7JTQI3KKL5KZ66.png?auto=webp&frame=1&width=1024&fit=bounds&md=2dfd90dae52a8d715e0517ed7fd8dc38)
5. The binaries' paths can by added by clicking on the ... and by selecting the binary file or by directly pasting the path in the space provided.   
6. The addresses of the binaries should be copied from the Readme document and pasted in the space provided.  
7. The SPI settings should be set as shown in the following image. The while the crystal frequency is board dependent, the SPI frequency should be set to 40MHz, SPI mode should be DIO, and flash size should be 8Mbit (1MB).   
![alt text](https://content.instructables.com/ORIG/FQK/45MZ/KKL5KZ65/FQK45MZKKL5KZ65.png?auto=webp&frame=1&width=1024&fit=bounds&md=7bfa593fcd5e44f5e41e2fa9b4bae99f)
8. From the COM port drop down menu, select the comport on which the NodeMCU/Wemos is connected. Also, set the baudrate to 1152000.
9. Finally, click on START. After a couple seconds, you should see a FINISH prompt in the same space where it reads IDLE.
10. Now the firmware has been successfully flashed. You can unplug the NodeMCU/Wemos and restart it.

### Configuring the NodeMCU
1. First time when the NodeMCU restarts after the flashing process, it will start in Access Point mode serving its own wireless network.    
2. Connect to the SUPLA network. it does not request for any password.    
3. Once connected, open a bowser and in the address bar type 192.168.1.4 and press enter.    
4. You will now be presented with the SUPLA configuration screen. Provide the WiFi credentials and the supla-dev credentials that we last saw in the "Prerequisites for the controller software/firmware" step.
![alt text](https://content.instructables.com/ORIG/F29/A2KM/KKL5KZTD/F29A2KMKKL5KZTD.png?auto=webp&frame=1&width=1024&fit=bounds&md=5e39ad590c2b63d9fdf77e248e375e93)   
5. After furnishing the details, click on SAVE and wait for the microcontroller to restart.

### Setting Up the Device
1. Login into the SUPLA console and click on the My SUPLA tab.    
2. In that window, the registration will be disabled by default. click on the box at the right top to enable registration and only then your strip controller will get listed here.    
![alt text](https://content.instructables.com/ORIG/FM1/C7DQ/KKL5L00W/FM1C7DQKKL5L00W.png?auto=webp&frame=1&width=1024&fit=bounds&md=b7d45f11a24774af61fc3285e9193cab)   

![alt text](https://content.instructables.com/ORIG/FFM/JENR/KKL5L02H/FFMJENRKKL5L02H.png?auto=webp&frame=1&width=1024&fit=bounds&md=3a72c7b5244e257d9231a757d15a070e)   
3. Once the device gets listed, click on that to bring up two yellow colored boxes.   
4. Click on each of them and under the Functions drop down, select the light type. One of the Functions should be RGB Color bulb and Dimmer.    
![alt text](https://content.instructables.com/ORIG/FX8/T2HM/KKL5L03Y/FX8T2HMKKL5L03Y.png?auto=webp&frame=1&width=1024&fit=bounds&md=1158ca21ea1b99faa12ccd00dca63d45)   
5. Click on save button to save the settings.

### Linking With Google Assistant
1. Open the Google Home app.    
2. At the top left, tap on + and then choose Set up device and then choose Works with Google.   
![alt text](https://content.instructables.com/ORIG/FNL/J2IA/KKL5L0KT/FNLJ2IAKKL5L0KT.png?auto=webp&frame=1&height=1024&fit=bounds&md=d0833e03ae79b711e0b67d1797bc8f66)     
3. Click on the search icon and search for the SUPLA app.
![alt text](https://content.instructables.com/ORIG/F50/9TV1/KKL5L0KU/F509TV1KKL5L0KU.png?auto=webp&frame=1&height=1024&fit=bounds&md=145031a20bedf8bad21105b7ad45823c)     
4. Select the SUPLA app and link it with Google by providing the credentials.   
5. After successful linking, the SUPLA devices should now get listed in the Home app.   

### Linking With Amazon Alexa
1. Open the Amazon Alexa app and tap on the More tab.   
![alt text](https://content.instructables.com/ORIG/F50/9TV1/KKL5L0KU/F509TV1KKL5L0KU.png?auto=webp&frame=1&height=1024&fit=bounds&md=145031a20bedf8bad21105b7ad45823c)    
2. Under More tab, tap on Skills and Games.    
3. Tap on the search icon and look for Supla Skill.   
![alt text](https://content.instructables.com/ORIG/F5Y/EIX7/KKL5L0VG/F5YEIX7KKL5L0VG.png?auto=webp&frame=1&height=1024&fit=bounds&md=940c90f8f94691070593443a74e35d84)     
4. Tap on Supla Skill and Enable it.
![alt text](https://content.instructables.com/ORIG/F0G/2WSJ/KKL5L0VE/F0G2WSJKKL5L0VE.png?auto=webp&frame=1&height=1024&fit=bounds&md=3e3d94edaa0e402cd1fb4e3f395fafa2)      
5. You will be prompted for SUPLA credentials and upon providing them, SUPLA will get linked to the Amazon Alexa Voice service.   
6. Choose the discover devices option. At the end of the discovery, the SUPLA devices should get listed in the Amazon Alexa devices option.    

### Demo
Amazon Alexa control   

[![Watch the video](https://img.youtube.com/vi/Ph3oHY7Yp_4/maxresdefault.jpg)](https://youtu.be/Ph3oHY7Yp_4)    

Google Assistant control    
[![Watch the video](https://img.youtube.com/vi/vpxPdPIRjG0/maxresdefault.jpg)](https://youtu.be/vpxPdPIRjG0)
