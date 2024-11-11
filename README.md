# DIY Feather v4 Standard Operating Procedures 

Bret Webb (bwebb@southalabama.edu)

GitHub: https://github.com/bwebb-southal/feathergauge 

DesignSafe: coming soon

## Arduino IDE Preparation
If you have zero experience using the Arduino IDE, please refer to these tutorials here: https://www.arduino.cc/en/Tutorial/HomePage

1. Enable support for Adafruit boards in the Preferences menu: https://learn.adafruit.com/adafruit-feather-m0-basic-proto/setup

1. Add support for the Adafruit AVR boards using Board Manager under Tools/Boards: https://learn.adafruit.com/adafruit-feather-32u4-adalogger/setup

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

![image]()

