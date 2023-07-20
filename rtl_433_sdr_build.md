Overview
This guide covers how to set up rtl_433 and MQTT to use an SDR dongle to sniff RF transmissions.

Activities
Install rtl_433 add on
Install Mosquitto MQTT Broker add on
Install the MQTT integration
Set up sensors
Optional split configuration file set up
INSTALL rtl_433 add on
In Home Assistant

Install rtl_433 add on
https://github.com/pbkhrv/rtl_433-hass-addons

run once to create rtl_433.conf.template in the config/rtl_433 folder

modify the rtl_433.conf.template file to configure rtl_433 to output data

more info here on config options: https://github.com/merbanan/rtl_433/blob/master
