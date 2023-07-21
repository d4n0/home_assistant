# **MQTT Binary Sensors**

At this point, you should have set-up Home Assistant on a Raspberry Pi and got the RTL-SDR picking up frequencies are 345 Mhz.

If your frequency detector is set up properly the log should look like:

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
[rtl_433] {"time" : "2023-07-20T16:47:13.379345-0500", "protocol" : 70, "model" : "Honeywell-Security", "id" : 75948, "channel" : 8, "event" : 160, "state" : "open", "contact_open" : 1, "reed_open" : 1, "alarm" : 0, "tamper" : 0, "battery_ok" : 1, "heartbeat" : 0, "mic" : "CRC", "mod" : "ASK", "freq" : 345.014, "rssi" : -0.126, "snr" : 8.352, "noise" : -8.478}
[rtl_433] {"time" : "2023-07-20T16:47:15.512281-0500", "protocol" : 70, "model" : "Honeywell-Security", "id" : 75948, "channel" : 8, "event" : 32, "state" : "closed", "contact_open" : 0, "reed_open" : 1, "alarm" : 0, "tamper" : 0, "battery_ok" : 1, "heartbeat" : 0, "mic" : "CRC", "mod" : "ASK", "freq" : 345.013, "rssi" : -0.082, "snr" : 8.714, "noise" : -8.796}
```

The output from our `rtl_433.conf.template` file should be publishing to the dynamic topic `homeassistant/devices[/model][/id]` and pushing the JSON to logs as seen above. You can use kv for a cleaner output but the JSON data will be used shortly and cuts out some steps.

## Run around opening doors and windows
If you have another person, this could be easier with oyu watching logs and them running around opening windows.
Most sensors will send several packets per state change, so if you are alone, only trigger a sensor or two before jotting down some information from the logs.

## Take Notes
Write down the following from the logs:
  - Model
  - ID
  - State (if different between being physically open and closed)
  - Contact_Open (if different between being physically open and closed)
  - Reed_Open (if different between being physically open and closed)
NOTE: Not all paramaters change and they are not always consistent between windows, doors, etc.

## Test MQTT Listener (Optional)
Since we already have the JSON data, this step would be to check that MQTT can pick up the sensor topic.
If you set output to kv, you can use this to note the sensors around your house.
  1. Navigate to MQTT integration
  2. Click `Configure`
  3. Add the topic you specified in `rtl_433.conf.template` (i.e., `homeassistant/events[/model][/id]`)
  4. Click `Start Listening`
