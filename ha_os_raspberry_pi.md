
# **INSTALL HOME ASSISTANT OPERATING SYSTEM**
This guide shows how to install the Home Assistant Operating system using Raspberry Pi Imager and was sourced from [https://www.home-assistant.io/installation/raspberrypi](url).
## **Write the image to your SD Card**
1. Download and install the Raspberry Pi Imager on your computer:
    - [https://www.raspberrypi.com/software/](url)
2. Open the Raspberry Pi Imager
3. Choose the operating system:
    - Select Other specific-purpose OS > Home assistants and home automation > Home Assistant
    - Choose the Home Assistant OS that matches your hardware (RPi 3 or RPi 4). Choose the operating system
4. Choose the storage:
    - Insert the SD card into the computer. Note: the contents of the card will be overwritten
5. Write the install to the SD card
6. Wait for the Home Assistant OS to be written to the SD card
7. Eject the SD card.

## **Start Raspberry Pi and Home Assistant**
1. Insert the SD card into your Raspberry Pi.
2. Plug in an Ethernet cable that is connected to the network.
3. Connect the power supply to start up the device.
4. After a few minutes, use the browser of your desktop system [homeassistant.local:8123](url)
    - Older Windows versions might need to access Home Assistant at `homeassistant:8123` or `http://X.X.X.X:8123`.
5. Follow on screen instructions to complete setup of Home Assistant OS
