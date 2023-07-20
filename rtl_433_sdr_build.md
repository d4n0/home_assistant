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

## **Configure rtl_433**
  1. From the rtl_4333 add-on screen, `START` the add-on
  2. Modify `/config/rtl_433/rtl_433.conf.template` to control RF settings
     For this build I used:

    #identifies device, required if using more than one SDR dongle
    device 0 
    
    #specifies output and included data
    output mqtt://${host}:${port},user=${username},pass=${password},retain=${retain},devices=homeassistant/devices/[/model] 
    [/id],events=homeassistant/events[/model][/id],states=homeassistant/states[/model][/id]
    report_meta time:iso:usec:tz
    report_meta level
    report_meta protocol
    
    #converts units to desired format
    convert customary
    
    #outputs table of device results to the log
    output json
    
    #specifies the frequency, can use more than one but then `hop_interval` in seconds is required
    frequency 344975000
    
    #protocols to avoid scanning for, this is the default list of TPMS (tire pressure sensors) to exclude. Helps eliminate 
    device noise from passing cars.
    protocol -59
    protocol -60
    protocol -82
    protocol -88
    protocol -89
    protocol -90
    protocol -95
    protocol -110
    protocol -123
    protocol -140
    protocol -156
    protocol -168
    protocol -180
    protocol -186
    protocol -201
    protocol -203 

    #protocol to ensure inclusion
    protocol 40
    protocol 70
    convert si
