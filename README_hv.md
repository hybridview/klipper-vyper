# Generic Klipper configuration

This generic Klipper configuration is designed for CoreXY printers. I use it on my Voron V2.4 (V2.1237), my Voron Trident, my custom TriZero, and my heavily modified Prusa i3 MK3s. Other printer owners (on Voron, VZbot, Ender5, ...) have also reported no issues using it.

This is a WIP: the files are frequently updated with new features that I create, but also with merged PRs from users. **Always** look, think, understand, and adjust to your own. But that should work in most cases. You can reach me in the Voron Discord: I'm **Frix_x#0161**.


## Features

This configuration is designed to be generic: you can use it on a wide variety of machines by simply selecting and enabling the hardware and software options that you need.

The **adaptive bed mesh** functionality I wrote some time ago, the **custom calibration macros** for pressure advance & flow, the **automated input shaper workflows**, and the **vibrations measurement** macros and scripts are among the custom features available out of the box.

Here is a [list with the details and usage instruction for all the features](./docs/features.md). There are also some installation instructions in their documentation if you want to use them standalone in your own personal configuration.


## Installation

Installing this configuration should not be too complicated if you are already familiar with the Klipper ecosystem. Here is how:
  1. First, make sure you have Klipper, Moonraker, and a WebUI is installed on your printer. You can use [KIAUH](https://github.com/th33xitus/kiauh) if you don't.
  2. To run the installation script, connect to your printer using SSH and type the following command:

     ```
     wget -qO /tmp/install.sh https://raw.githubusercontent.com/hybridview/klipper-vyper/main/install.sh && bash /tmp/install.sh
     ```
  
  3. This will backup your old configuration, download this repo into your home directory and install the environment in your `~/printer_data/config` folder. You'll also be asked if you want to select and install some MCU board_pins templates. This is recommended as it will allow a very quick filling of your `mcu.cfg` user file, but you can always do it manually afterwards if you prefer (see [MCU pinout and wiring documentation](./docs/pinout.md)).
  4. Add the serial_port and/or can_uuid of your MCUs to the `mcu.cfg` file. Please refer to the [official klipper documentation](https://www.klipper3d.org/FAQ.html#wheres-my-serial-port) to find them.
  5. Open the `printer.cfg` file and uncomment the lines that correspond to your printer hardware in order to enable the required components and software (such as extruder type, XY motors, Z motors, QGL vs Z_TILT, etc...).
  6. Then it's time to customize the configuration by editing the `overrides.cfg` user file. For example, you can tweak the dimensions, limits, currents, and all the other values from all config sections. **Pay special attention to the axis limits** in the `[stepper_...]` sections (files located in [config/hardware/axis](./config/hardware/axis/)). Also check the thermistor types in `[extruder]` and `[heated_bed]`, the plate size in `[bed_mesh]`, and so on. Include any modifications in your `overrides.cfg` and **never modify my config directly** as they will be deleted when the repo updated!
  7. Modify and adapt the `variables.cfg` file to suit the configuration of your machine. This file helps to configure and customize how all the macros should behave (coordinates of everything, enable/disable some software features, etc...).
  8. **Check all features very carefully to avoid any problems on your machine!** You can follow the [config checks from the official Klipper documentation](https://www.klipper3d.org/Config_checks.html). Then, also check that you are able to attach/detach the mechanical probe (if you use one), do the QGL/Z_TILT, have correct coordinates for all the components used (purge bucket, physical Z endstop, etc...). You should also check your first layer calibration (and the `switch_offset` parameter of the automatic z calibration plugin if you use it), etc...
  9. Finally when everything seems to work, you need to add the custom print start gcode to your slicer. Here is an example for SuperSlicer:
     
     ```
     START_PRINT EXTRUDER_TEMP={first_layer_temperature[initial_extruder] + extruder_temperature_offset[initial_extruder]} BED_TEMP=[first_layer_bed_temperature] MATERIAL=[filament_type] CHAMBER=[chamber_temperature] SIZE={first_layer_print_min[0]}_{first_layer_print_min[1]}_{first_layer_print_max[0]}_{first_layer_print_max[1]}
     ```
     
     Also add the custom print end gcode to your slicer:

     ```
     END_PRINT
     ```


## Sponsor the work

I try to be open to any user request if it fits into this configuration design. So feel free to open an issue or a PR if you want your specific hardware device or new feature to be supported.

Alternatively, you can also buy me a coffee or help me buy new hardware to support my work :)
