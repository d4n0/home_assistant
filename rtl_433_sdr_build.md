## **Description**
This guide covers how to set up rtl_433 and MQTT to use an SDR dongle to sniff RF transmissions.
- The build utilizes pbkhrv's [rtl_433-hass-addons](https://github.com/pbkhrv/rtl_433-hass-addons) that are based on merbanan's [rtl_433](https://github.com/merbanan/rtl_433) project that uses RTL-SDR or SoapySDR. Some links and configurations are derived from recommendations within their projects.

## **Steps**
  - Load Custom Repository
  - Install Add-ons
  - Configure rtl_433
  - Configure MQTT

## **Load Custom Repository**
Following the instructions for [adding a custom repository](https://www.home-assistant.io/common-tasks/os#installing-third-party-add-ons):
   - Add https://github.com/pbkhrv/rtl_433-hass-addons to HA

## **Install Add-ons**
With the repository loaded, you should see a new list of items at the bottom of the Add-on Store.
  1. Click `Settings`
  2. Click `Add-ons`
  3. Click `ADD-ON STORE` in the bottom right
  4. Search for and install `rtl_433` add-on
  5. Search for and install `Mosquitto broker` add-on


