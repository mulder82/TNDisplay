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
3. Connect display and upload project ([see instructions](https://www.youtube.com/watch?v=xgBq5L0nSWk))
# Wemos D1 module
1. Flash ESP module with Tasmota ([see instructions](https://tasmota.github.io/docs/Getting-Started/#needed-software))
2. Configure Tasmota (set WiFi connection, [MQTT](https://tasmota.github.io/docs/MQTT/#configure-mqtt)) and use following [template](https://tasmota.github.io/docs/Templates/)
```console
{"NAME":"TNDisplay","GPIO":[0,0,320,0,0,0,0,0,0,0,0,0,0,0],"FLAG":0,"BASE":18}
```
MQTT Settings | Template Settings
--- | ---
![Screenshot](https://github.com/mulder82/TNDisplay/blob/main/Tasmota/mqtt.JPG) | ![Screenshot](https://github.com/mulder82/TNDisplay/blob/main/Tasmota/template.JPG)

4. Set Tasmota rule to initialize communication and show informations when connecting/disconnecting wifi and mqtt. Open tasmota console and execute following command:
```console
Rule1 ON System#Init DO serialsend5 64696d3d313030ffffff ENDON ON Wifi#Connected DO serialsend5 706167652036ffffff54312e7478743d2257494649204f4b22ffffff50312e7069633d3237ffffff ENDON ON Wifi#Disconnected DO serialsend5 706167652036ffffff54312e7478743d2257494649204f46464c494e4522ffffff50312e7069633d3531ffffff ENDON ON Mqtt#Connected DO serialsend5 706167652036ffffff54312e7478743d224d515454204f4b22ffffff50312e7069633d3236ffffff ENDON ON Mqtt#Disconnected DO serialsend5 706167652036ffffff54312e7478743d224d515454204f46464c494e4522ffffff50312e7069633d3434ffffff ENDON
```
4. Enable Rule1 by executing command:
```console
Rule1 1
```
5. Connect ESP module with Nextion display:

> [!WARNING]  
> Disconnect power supply when making connections!

Nextion PIN | ESP Pin
--- | ---
+5V (black) | 5V
TX (red) | RX
RX (white) | TX
GND (yellow) | G

> [!IMPORTANT]  
> Note the crossover RX TX pins
   
7. At this stage if you have done everything correctly after restarting tasmota the screen should sequentially show the information "WiFi OK", "MQTT OK"

# NodeRed
1. Import node red [flow file](https://github.com/mulder82/TNDisplay/blob/main/NodeRed/TNDisplay.json) [see instructions](https://nodered.org/docs/user-guide/editor/workspace/import-export)
2. Check the settings, mainly that the topics in the MQTT nodes match those you set in Tasmota, and that the MQTT configuration node is configured correctly.
3. At this stage, if you have done everything correctly, after deploy flow in NodeRed the display should show the demo application.
