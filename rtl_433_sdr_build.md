## **Description**
This guide covers how to set up rtl_433 and MQTT to use an SDR dongle to sniff RF transmissions.
- The build utilizes pbkhrv's [rtl_433-hass-addons](https://github.com/pbkhrv/rtl_433-hass-addons) that are based on merbanan's [rtl_433](https://github.com/merbanan/rtl_433) project that uses RTL-SDR or SoapySDR. Some links and configurations are derived from recommendations within their projects.

## **Steps**
  - Load Custom Repository
  - Install Add-ons
  - Configure rtl_433
  - Configure MQTT
  - Restart Home Assistant

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
  1. Plug in SDR dongle. I used a [Nooelec NESDR Nano 2](https://www.nooelec.com/store/nesdr-nano2.html)
  1. From the rtl_4333 add-on screen, ensure all three toggles are on
     NOTE: This will keep the add-on up-to-date and running
  2. Click `START`
  3. Modify `/config/rtl_433/rtl_433.conf.template` to control RF settings
     For this build I used:
```
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

#protocols to ensure inclusion
protocol 40
protocol 70
convert si
```
## **Configure MQTT**
The MQTT set-up has two parts: The Broker and the Integration
1. Configure Mosquitto MQTT Broker
   - Add user to configuration tab 'Logins' section
        ```
        - username: [username]
        password: [passwd]
        ```
    - Ensure the same three toggles are on here as well
    - `START` add-on
2. Install/Configure MQTT Integration
   - The integrations should appear automatically when you navigate to the integrations page.
       a. Click `CONFIGURE`
       b. MQTT should zeroconf configure and pull necessary information from Mosquitto MQTT
   - If zeroconf fails, add/search for MQTT from the integrations page.
       a. Click `INSTALL`
       b. Fill out the Broker Options from the Mosquitto MQTT configuration

## **Restart Home Assistant**
1. From settings, click three dots
2. Select `Restart Home Assistant`
3. Select Advanced options dropdown
4. Click `Reboot System`

It will take a few minutes to restart, but afterwards go to `Settings > System > Logs`

# Set-up COMPLETE!!!

If the set-up was successful, your logs (receachable through the top right drop down) should look similar to the following:

#### Home Assistant Core
```
There are no new issues!
```

#### Mosquitto broker
```
s6-rc: info: service s6rc-oneshot-runner: starting
s6-rc: info: service s6rc-oneshot-runner successfully started
s6-rc: info: service fix-attrs: starting
s6-rc: info: service fix-attrs successfully started
s6-rc: info: service legacy-cont-init: starting
cont-init: info: running /etc/cont-init.d/mosquitto.sh
[hh:mm:ss] INFO: Setting up user mqttuser
[hh:mm:ss] INFO: SSL is not enabled
cont-init: info: /etc/cont-init.d/mosquitto.sh exited 0
cont-init: info: running /etc/cont-init.d/nginx.sh
cont-init: info: /etc/cont-init.d/nginx.sh exited 0
s6-rc: info: service legacy-cont-init successfully started
s6-rc: info: service legacy-services: starting
services-up: info: copying legacy longrun mosquitto (no readiness notification)
services-up: info: copying legacy longrun nginx (no readiness notification)
s6-rc: info: service legacy-services successfully started
[hh:mm:ss] INFO: Starting NGINX for authentication handling...
[hh:mm:ss] INFO: Starting mosquitto MQTT broker...
[hh:mm:ss] INFO: Successfully send discovery information to Home Assistant.
[hh:mm:ss] INFO: Successfully send service information to the Supervisor.
```

#### rtl_433
```
s6-rc: info: service s6rc-oneshot-runner: starting
s6-rc: info: service s6rc-oneshot-runner successfully started
s6-rc: info: service fix-attrs: starting
s6-rc: info: service fix-attrs successfully started
s6-rc: info: service legacy-cont-init: starting
s6-rc: info: service legacy-cont-init successfully started
s6-rc: info: service legacy-services: starting
s6-rc: info: service legacy-services successfully started
Starting rtl_433 with rtl_433.conf...
[rtl_433] rtl_433 version 22.11 branch  at 202211191645 inputs file rtl_tcp RTL-SDR
[rtl_433] Use -h for usage help and see https://triq.org/ for documentation.
[rtl_433] Publishing MQTT data to core-mosquitto port 1883
[rtl_433] Publishing device info to MQTT topic "homeassistant/devices[/model][/id]".
[rtl_433] Publishing events info to MQTT topic "homeassistant/events[/model][/id]".
[rtl_433] Publishing states info to MQTT topic "homeassistant/states[/model][/id]".
[rtl_433] Registered 178 out of 223 device decoding protocols [ 1-4 8 11-12 15-17 19-23 25-26 29-36 38-58 63 67-71 73-81 83-87 91-94 96-100 102-105 108-109 111-116 119 121 124-128 130-139 141-149 151-155 157-161 163-167 170-175 177-179 181-185 187-197 199 202 204-215 217-223 40 70 ]
[rtl_433] Found Rafael Micro R820T tuner
[rtl_433] Exact sample rate is: 250000.000414 Hz
[rtl_433] [R82XX] PLL not locked!
[rtl_433] Sample rate set to 250000 S/s.
[rtl_433] Tuner gain set to Auto.
[rtl_433] Tuned to 344.975MHz.
[rtl_433] Allocating 15 zero-copy buffers
[rtl_433] baseband_demod_FM: low pass filter for 250000 Hz at cutoff 25000 Hz, 40.0 us
[rtl_433] MQTT connect error: Connection refused
[rtl_433] MQTT Connected...
[rtl_433] MQTT Connection established.
```
