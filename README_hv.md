
### 20231207: I think this is ready to try in real printer...

### ABM NOTE: I think only custom thing here is the wget that points to diff repo.

# Where I left off (For when I take a long break from this.)

I don't think this is installed to any of my printers yet.


# Added Features

* Support for the Anycubic Vyper
* Support for rpi 2040 and mpu9250 accelerometer.
* WIFI power relays using MQTT.




To run the installation script, connect to your printer using SSH and type the following command:

     ```
     wget -qO /tmp/install.sh https://raw.githubusercontent.com/hybridview/klipper-vyper/main/install.sh && bash /tmp/install.sh
     ```
  