# Overview
This guide covers how to set up rtl_433 and MQTT to use an SDR dongle to sniff RF transmissions.
- The build utilizes pbkhrv's [rtl_433-hass-addons](https://github.com/pbkhrv/rtl_433-hass-addons) that are based on merbanan's [rtl_4333](https://github.com/merbanan/rtl_433) project that uses RTL-SDR or SoapySDR.

## Steps
1. Install rtl_433 add on
2. Install Mosquitto MQTT Broker add on
3. Install the MQTT integration

INSTALL rtl_433 add on
In Home Assistant

Install rtl_433 add on
https://github.com/pbkhrv/rtl_433-hass-addons

run once to create rtl_433.conf.template in the config/rtl_433 folder

modify the rtl_433.conf.template file to configure rtl_433 to output data

more info here on config options: https://github.com/merbanan/rtl_433/blob/master
