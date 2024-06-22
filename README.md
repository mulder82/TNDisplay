# TNDisplay
The goal of the project is to create a wireless touchscreen display that can be programmed using NodeRed.
1|2|3 
--- | --- | ---
![Screenshot](https://github.com/mulder82/TNDisplay/blob/main/_media/tndisplay.jpg)|![Screenshot](https://github.com/mulder82/TNDisplay/blob/main/_media/wiring/wiring1.jpg)|![Screenshot](https://github.com/mulder82/TNDisplay/blob/main/_media/wiring/wiring2.jpg)
# Requirements
## Hardware
1. Nextion HMI Display, model [NX3224T024](https://nextion.tech/basic-series-introduction/) or other Nextion display with resolution 320x240px
2. [Wemos D1 mini lite](https://www.wemos.cc/en/latest/d1/d1_mini_lite.html) or other ESP MCU with 5v power pin
## Software
1. MQTT broker (see [mosquitto](https://mosquitto.org/download/))
2. Node-Red  (see [getting started with node-red](https://nodered.org/docs/getting-started/))
# Configuration
## Nextion display (upload TFT project)
### Option A (using SDCard)
To upload TFT project using SDCard use [TNDisplay.tft](https://github.com/mulder82/TNDisplay/blob/main/Nextion/TNDispay.tft) file and follow [this instructions](https://nextion.tech/faq-items/using-nextion-microsd/)
### Option B (using ttl adapter)
1. Download and install [NextionEditor](https://nextion.tech/nextion-editor/#_section1)
2. Download [TNDisplay.hmi](https://github.com/mulder82/TNDisplay/blob/main/Nextion/TNDispay.HMI)
3. Connect display and upload project [see instructions](https://www.youtube.com/watch?v=xgBq5L0nSWk)
# Wemos D1 module
1. Flash ESP module with Tasmota [see instructions](https://tasmota.github.io/docs/Getting-Started/#needed-software)
2. Configure Tasmota (set WiFi connection and [MQTT](https://tasmota.github.io/docs/MQTT/#configure-mqtt)
3. Set Tasmota rule to initialize communication and show informations when connecting/disconnecting wifi and mqtt. Open tasmota console and execute following command:
```console
Rule1 ON System#Init DO serialsend5 64696d3d313030ffffff ENDON ON Wifi#Connected DO serialsend5 706167652036ffffff54312e7478743d2257494649204f4b22ffffff50312e7069633d3237ffffff ENDON ON Wifi#Disconnected DO serialsend5 706167652036ffffff54312e7478743d2257494649204f46464c494e4522ffffff50312e7069633d3531ffffff ENDON ON Mqtt#Connected DO serialsend5 706167652036ffffff54312e7478743d224d515454204f4b22ffffff50312e7069633d3236ffffff ENDON ON Mqtt#Disconnected DO serialsend5 706167652036ffffff54312e7478743d224d515454204f46464c494e4522ffffff50312e7069633d3434ffffff ENDON
```
4. Enable Rule1 by executing command:
```console
Rule1 1
```
5. Connect ESP module with Nextion display:

Nextion PIN | ESP Pin
--- | ---
+5V (black) | 5V
TX (red) | RX
RX (white) | TX
GND (yellow) | G
   
7. At this stage if you have done everything correctly after restarting tasmota the screen should sequentially show the information "WiFi OK", "MQTT OK"




> [!IMPORTANT]  
> Place downloaded files under /config/www/immich-slideshow/ directory.

# Immich server configuration
1. Login into your immich server and create new apiKey

![Screenshot](https://github.com/mulder82/immich-slideshow/raw/master/screenshots/apikey.jpg)

# HomeAssistant configuration
1. Login into HomeAssistant server and add new custom card to the dashboard with the following configuration parameters:

Parameter name | Required | Default value | Description
--- | --- | ---- | ---
host | YES | - | URL to immich server
apikey | YES | - | Immich apiKey
slideshow_interval | NO | 6 | Time (in seconds) after new image is loaded (minimum 6)
height| NO | auto | Card height (eg. 500px)

# Preview in chromium browser
Run chromium using following commands:

1. Linux:

```console
/usr/bin/chromium-browser --noerrdialogs --disable-infobars --ignore-certificate-errors --allow-running-insecure-content --disable-web-security --user-data-dir=PATH_TO_PROFILE_DIRECORY --kiosk DASHBOARD_URL
```

2. Windows:
```console
start "C:\Program Files\Google\Chrome\Application\" chrome.exe --allow-running-insecure-content --disable-web-security --user-data-dir=PATH_TO_PROFILE_DIRECORY --kiosk DASHBOARD URL
```
> [!TIP]
> Replace PATH_TO_PROFILE_DIRECORY and DASHBOARD_URL with valid values.
