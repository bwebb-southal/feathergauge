# DIY Feather v4 Standard Operating Procedures 

Bret Webb (bwebb@southalabama.edu)

GitHub: https://github.com/bwebb-southal/feathergauge 

DesignSafe: coming soon

## Arduino IDE Preparation
If you have zero experience using the Arduino IDE, please refer to these tutorials [here](https://www.arduino.cc/en/Tutorial/HomePage)

1. Enable support for Adafruit boards in the Preferences menu by following [these directions](https://learn.adafruit.com/adafruit-feather-32u4-adalogger/setup)

1. Add support for the Adafruit AVR boards using Board Manager under Tools/Boards using [these instructions](https://learn.adafruit.com/adafruit-feather-32u4-adalogger/setup)

1. Select the Adafruit Feather 32u4 under Tools / Board

1. If this is your first time setting up your Arduino environment, you’ll need to add the necessary libraries. Libraries are managed using Tools / Manage Libraries in the Arduino IDE. The Nov2024 versions of the logger code sketches are compatible with the following libraries, and all of these need to be installed on your computer:

    a. Blue Robotics MS5837 v1.1.1

    b. SD v1.3.0

    c. RTClib v2.1.4

    d. TimerOne v1.1.1

1. Add the logger code sketch to your default Arduino Sketchbook location folder… note that the code sketch must reside in a folder of the same name as the sketch… this is required! The Arduino Sketchbook location folder was established during the setup process when you installed the Arduino IDE software. However, it can be redefined at any time. This is defined in your Arduino IDE Preferences menu (File / Preferences).

1. Ensure device is recognized in Tools/Port and select it. If you do not see your device, refer to Troubleshooting below. 

>[!NOTE]
> Ensure that your files and software are installed on your computer and not in a cloud-based segment of your PC or Mac. We have observed inconsistent behavior when using cloud-based folders. Note that many new PCs, specifically laptops, will default to cloud-based or cloud-connected folders on your system. If your Arduino Sketchbook location folder is not defined in a path structure on your physical hard drive, things may not work very well.



## Deployment Preparation 
Here are step-by-step instructions for preparing a DIY Feather v4 wave gauge for deployment. These steps assume that you already have your Arduino and environment prepared. If this is your first time using the gauge, please refer to the section at the end of this document regarding Arduino IDE Preparation. 

1. charge the battery (plug the battery into the USB charging adapter, or plug the battery into the board and then plug the board into a computer or USB outlet)

1. check the RTC
   
    a. Connect the board to the computer
  
    b. Open the Arduino software
  
    c. Open the sketch File/Examples/RTClib/ds3231
  
    d. Compile and upload the sketch to your board
  
    e. Open the serial monitor in the Arduino IDE (Tools / Serial Monitor) and confirm the date and time
  
    f. If the date/time is incorrect, uncomment line #25 then repeat steps 2d and 2e
  
    g. If the clock is still not correct, proceed to 3 below

1. reset the RTC

    a. remove coin cell battery for at least 60 seconds then replace it
  
    b. repeat steps 2c-2e

1. upload logger sketch

    a. There are four possible logger sketches as of Nov 2024: 1) rapid start with user-defined sampling rate; 2) delayed start with user-defined sampling rate; 3) rapid start with burst sampling; 4) delayed start with burst sampling
  
    b. Be sure to define your desired parameter values in the /* User Inputs */ section of each code sketch

1. allow DIY gauge to sample for about 60 s

1. disconnect usb 

1. remove microsd

1. insert microsd card into your computer

1. check data file and confirm that date/time and pressure (and/or temperature) are correct

1. remove data file(s)

1. reinsert microsd card into board


## Deployment 
When you are ready to deploy the gauge, follow these steps…

1. plug in the battery 

1. confirm LED flashing* (as of versions labeled _v1):

    a. rapid start, continuous sampling: solid green for about the first ~10 seconds then no other LEDs

    b. Rapid start, burst sampling: solid green during burst sampling; solid red during sleep interval 

    c. delayed start, continuous sampling: flashing red for ~20 seconds before start time; solid green for about the first ~10 seconds of continuous sampling

    d. delayed start, burst sampling: flashing red for ~20 seconds before start time; solid green during burst sampling; solid red while sleeping in between bursts

1. insert components into gauge housing along with a small desiccant pack

1. allow to sample** in atmospheric pressure for at least 1-2 minutes

1. place all prepared gauges in a bucket filled with your seawater (preferably from your deployment location but freshwater will do) and allow to sample** for at least 1-2 minutes. Ensure all sensors are oriented similarly (sensor at the bottom of the bucket).
   
1. deploy sensor making sure you keep depth attenuation in mind… see guidance below.

    a. Basically, you need to ensure your pressure sensor will detect the dynamic pressure fluctuations of your shortest wave periods, which attenuate quickly over the water column. 

    b. Figure 1 below shows the pressure decay coefficient as a function of wave period and water depth for four different deployment elevations (above the bed). You want to keep your decay coefficient as close to 1 as possible. You definitely want to stay out of the blue areas in these figures.

    c. Example: if you deploy a gauge on the bed in 3 m of water, you won’t detect any dynamic pressure (or hardly any) for wave periods less than or equal to 2 s. 

1. recommend deploying the gauge horizontally or vertically, and if vertically do so with sensor port pointing downward 

>[!NOTE]
> In step 2: if you would like to conserve more battery power, disabling the LED flashing is a fairly simple task. Any/all commands labeled “digitalWrite(----)” within the void loop() structure can be commented out with no impact to the code operation whatsoever. To comment (i.e., disable) out the LED blinking, simply place your cursor on the line of code (to the left of) containing the active digitalWrite(8, xxx) or digitalWrite(13, xxx) command, then select Edit / Comment/Uncomment from the Arduino IDE menu. If the line is active, it will become inactive, you’ll see  two “//” before the statement, and the text will turn gray. To reactivate that line of code, either remove the “//” or select Edit / Comment/Uncomment again and the line of code will become active once again.

>[!NOTE]
> In steps 4-5: this only makes sense if you are using the rapid start version of the logger code sketches. If you are using the rapid start code with burst sampling, make sure you are logging atmospheric and bucket test pressures during your burst interval (refer to LED flashing codes above for reference). If you are using the delayed start version of the code sketches, it may not be possible to sample atmospheric or bucket test pressures prior to deployment. If that is the case, I strongly recommend doing these things at the end of your deployment (before removing the battery). The atmospheric and bucket test pressure samples allow you to perform minor corrections to ensure consistent measurement values across your gauges. The inexpensive pressure sensors seem to have small offsets that, while not necessary, could be advantageous to correct by comparing their values under static conditions.


![pressuredecayguide](https://github.com/user-attachments/assets/69788a87-37ee-42d7-9b7c-4da35f923b32)
Figure 1. Deployment Guidance for Pressure Attenuation with Depth


## Post-Deployment Recovery
Here are some suggested step-by-step procedures to consider after you retrieve your DIY wave gauge…

1. do not open gauge before cleaning thoroughly 

1. submerge gauge in a bucket of warm water mixed with distilled white vinegar (and dish soap if you like, but the dish soap is not necessary)

1. if gauges are considerably fouled, consider adding baking soda as this will combine with the vinegar to produce strong agitation and fizzing (definitely do not use dish soap here)

1. do not touch the gel membrane inside of the pressure sensor no matter what you do 

1. remove from cleaning bath and wipe dry

1. remove cap 

1. inspect for signs of moisture 

1. remove internal components 

1. disconnect battery 

1. remove microsd card

## Post-Processing 
The gauge data will be saved to CSV files on the microsd card. Post-processing the pressure data can be done in a variety of ways. We have posted some example post-processing scripts written in MATLAB. If you don’t have access to MATLAB you might find your own alternative method for processing the data. Just remember that the pressure values are absolute… so you need to subtract out atmospheric pressure. Ideally, you would have an atmospheric reference nearby so that you have a time-series of data, but in a pinch you can use an average/estimated value of atmospheric pressure. Each millibar of atmospheric pressure corresponds to (approximately) 1 cm of water height change. 

1. insert microsd card into your computer 

1. save the files to your computer

1. run the MATLAB post-processing scripts or process using your own codes


## Troubleshooting

1. My board isn’t recognized by Arduino IDE: make sure you are using a power+data cable… many micro USB cables are power only… if the device is not recognized as a com port under device manager (windows) then you’re probably using a power only cable.

1. My board isn’t recognized by Arduino IDE and I am sure that I am using an appropriate power+data cable: try resetting the bootloader on the feather logger board (see below).

1. I need to reset my bootloader: you’ll need access to the small black reset button located near the micro USB plug on top of the board. With the board plugged in, open the blink sketch found in File / Examples / Basics / Blink. Click the compile/upload “arrow” icon. Immediately double tap the reset button. This should resolve the issue. You may need to do this a few times. 

1. My date/time are incorrect: refer to 2 and 3 in the Deployment Preparation section above.

1. My logger isn’t working correctly: try uploading something simple like File / Examples / Basics / Blink. Does that work? If not, there’s likely an issue with your board. If yes, see below.

1. My logger still isn’t working: 

    a. Check your microsd card. Is it installed correctly? Are you using the recommended 8gb microsd card? If not, this may be the issue. The logger cannot handle large microsd cards.

    b. Check your wiring. 

    c. Perform a continuity check.

1. My logger is writing to the microsd card, but the values don’t make sense.

    a. Check your wiring… make sure you did not reverse the SCL and SDA wires.

    b. Try using the simple sketch provided by the MS5837 pressure sensor manufacturer by going to File / Examples / BlueRobotics MS5837 Library / MS5837_example. Before uploading, you’ll need to change one line in the code. Refer to the line with…

    ```
      sensor.setModel(MS5837::MS5837_30BA);
    ```
    and change the _30BA to _02BA as follows…
    ```
	    sensor.setModel(MS5837::MS5837_02BA);
    ```
    then open Serial Monitor and see if the values make sense.

1. open for addressing future issues…


