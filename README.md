# DJI_FPV_ANALOG
Analog diversity receiver, wifi controlled, fitted inside DJI FPV Googles


this project is published for personal use, you can produce and use as many as you want for private use
If you do produce this for commercial purposes, eg. selling this , you're not allowed to do. 
please contact developer if you're interested in this a defilippis1962@gmail.com


DJI ANALOG DIVERSITY MODULES


This boards are made to be fitted inside DJI FPV GOOGLES

Power and video/audio can be taken directly from inside the googles or by cables from outside

Requires two antennas, connected to boards using a uFl connector (one for each board)

Boards control is achieved via wifi connection. Once powered you need to connect to the device in wifi connections,
then start the app and gain control

At present time app runs ONLY in Android. a IOS solution can be provided but it takes time, I will only if the project
will have commercial development

Project use RX5808 modules, opened and modified to work directly at 3V3. 
This means that the internale voltage regulator must be removed and replaced with a small wire from input to output

This modules runs at 3V3 internally, powering at 3V3 reduces power requirements and keeps modules much cooler

Also, you need to check that the data control lines does not have any resistor placed. 
As you need to open the modules to remove the power regulator, you can also check for resistors and in case, remove them

Schematics: description

Main board. 
There is a dc/dc voltage regulator. high efficiency, very low noise, input from 9 up to 36V, 3V3 vout, 1A
All devices on board are 3V3 powered

MCU. it is a Microchip 18F25K22 in QFN footprint. care must be taken in welding

Video Mux: TS5A3154DCUR . this is a dedicate video switch device, to reduce spikes in channel changes. made by Texas Instruments

there are some resistors and caps on board. an inductor also on input part of a low pass filter.

RSSI signal comes from the modules changing from 0.5 (lower rssi) up to 1.2V (higher rssi, saturation)
To enlarge A/D conversion for the MCU (10 bit)  the resistor ladder made by R2-R3-R4 sets proper voltages for 
Vref+  and Vref-  just to have around 1000 steps of resolution for rssi signal
There's a 10 pole ZIF connector for the other board, carrying all the necessary signals

slave board:

there is just the other receiver and the wifi module on this slave board. connected to main board with the ZIF connector


Firmware

Firmware allows to set some parameters and to perform some tasks
Settings:
you can choose to start the modules retriving the last channel or to start with an autoscan to search for higher rssi value

Please keep in mind that to perform a good autosearch, Vtx must be at least 5 meters away, otherwise it will saturate also nearby channels 
resulting in a bad setting. (eg. frequency to be selected 5865, vtx too close it will have a similar signal also for 5870 resulting in a wrong selection)

you can set the hysteresis for switching between one channel to the other. default 10%.
this means that if the difference between the two receiver's rssi values is LESS than 10%, no receiver switch occurs

Low Set: this set the limit below that even a 1% difference in rssi signals causes receiver changes
High set: this set the limit above that no changes occurs for any reasons

Modules must be 'aligned' at first (just one time)

Set the modules in the correct channel with a VTX on, place the VTX 5 meters away and using the app, perform HIGH RSSI setting
Then in the same condition, turn off vtx. be careful not to have other vtx on in the nearings. from APP select the LOW RSSI setting
 to enter this settings, long tap on SETUP in main page, then long tap on SETTINGS on setup page
 
 

The wifi name can be changed (apart from the initial DJI_FPV_) in the app. 
There is also a password. this is necessary to stop someone else with the app installed to connect to your googles and play with your channels
dangerous expecially if you're flying ;-)


password default is 0000  . if you forget it, you can boot the device shortening the two pads on the main board, this resets all data to factory default. means you have to redo the max/min rssi procedure

SCAN mode

Scanning is made checking all available channels (analog and DJI digital) providing a 'visual' situation of free frequencies on site
All the channels marked with a red dot are somehow affected by some transmission. this means that rssi on this channels is higher than 5%
When a channel is totally free, rssi is 0%

After scanning you will be able to select a totally free channel very easily








