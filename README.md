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
1. Import node red [flow file](https://github.com/mulder82/TNDisplay/blob/main/NodeRed/TNDisplay.json)  [(see instructions)](https://nodered.org/docs/user-guide/editor/workspace/import-export)
2. Check the settings, mainly that the topics in the MQTT nodes match those you set in Tasmota, and that the MQTT configuration node is configured correctly.
3. At this stage, if you have done everything correctly, after deploy flow in NodeRed the display should show the demo application.

# Casing
If you want to print the casing, use the project files included in the [Casing](https://github.com/mulder82/TNDisplay/tree/main/Casing) folder.
![Screenshot](https://github.com/mulder82/TNDisplay/blob/main/_media/casing/3dPrint.jpg)

# Available Pages

0 | 1 | 2 | 3 | 4
--- | --- | --- | --- | ---
![Screenshot](https://github.com/mulder82/TNDisplay/blob/main/_media/nextion/pages/Page0.JPG) | ![Screenshot](https://github.com/mulder82/TNDisplay/blob/main/_media/nextion/pages/Page1.JPG) | ![Screenshot](https://github.com/mulder82/TNDisplay/blob/main/_media/nextion/pages/Page2.JPG) | ![Screenshot](https://github.com/mulder82/TNDisplay/blob/main/_media/nextion/pages/Page3.JPG) | ![Screenshot](https://github.com/mulder82/TNDisplay/blob/main/_media/nextion/pages/Page4.JPG)

5 | 6 | 7 | 8 | 9
--- | --- | --- | --- | ---
![Screenshot](https://github.com/mulder82/TNDisplay/blob/main/_media/nextion/pages/Page5.JPG) | ![Screenshot](https://github.com/mulder82/TNDisplay/blob/main/_media/nextion/pages/Page6.JPG) | ![Screenshot](https://github.com/mulder82/TNDisplay/blob/main/_media/nextion/pages/Page7.JPG) | ![Screenshot](https://github.com/mulder82/TNDisplay/blob/main/_media/nextion/pages/Page8.JPG) | ![Screenshot](https://github.com/mulder82/TNDisplay/blob/main/_media/nextion/pages/Page9.JPG)

# Available Icons
## 50x50px (for use in header (PH.pic))

11 | 12 | 13 | 14 | 15 | 16 | 17 | 66 | 67 | 68 | 69
-- | -- | -- | -- | -- | -- | -- | -- | -- | -- | --
![Screenshot](https://github.com/mulder82/TNDisplay/blob/main/_media/nextion/icons/50/11.png) | ![Screenshot](https://github.com/mulder82/TNDisplay/blob/main/_media/nextion/icons/50/12.png) | ![Screenshot](https://github.com/mulder82/TNDisplay/blob/main/_media/nextion/icons/50/13.png) | ![Screenshot](https://github.com/mulder82/TNDisplay/blob/main/_media/nextion/icons/50/14.png) | ![Screenshot](https://github.com/mulder82/TNDisplay/blob/main/_media/nextion/icons/50/15.png) | ![Screenshot](https://github.com/mulder82/TNDisplay/blob/main/_media/nextion/icons/50/16.png) | ![Screenshot](https://github.com/mulder82/TNDisplay/blob/main/_media/nextion/icons/50/17.png) | ![Screenshot](https://github.com/mulder82/TNDisplay/blob/main/_media/nextion/icons/50/66.png) | ![Screenshot](https://github.com/mulder82/TNDisplay/blob/main/_media/nextion/icons/50/67.png) | ![Screenshot](https://github.com/mulder82/TNDisplay/blob/main/_media/nextion/icons/50/68.png) | ![Screenshot](https://github.com/mulder82/TNDisplay/blob/main/_media/nextion/icons/50/69.png)

## 70x70px (for use as buttons images (P1.pic, P2.pic etc.)

18 | 19 | 20 | 21 | 22 | 23 | 24 | 25 | 26 | 27
-- | -- | -- | -- | -- | -- | -- | -- | -- | --
![Screenshot](https://github.com/mulder82/TNDisplay/blob/main/_media/nextion/icons/70/18.png) | ![Screenshot](https://github.com/mulder82/TNDisplay/blob/main/_media/nextion/icons/70/19.png) | ![Screenshot](https://github.com/mulder82/TNDisplay/blob/main/_media/nextion/icons/70/20.png) | ![Screenshot](https://github.com/mulder82/TNDisplay/blob/main/_media/nextion/icons/70/21.png) | ![Screenshot](https://github.com/mulder82/TNDisplay/blob/main/_media/nextion/icons/70/22.png) | ![Screenshot](https://github.com/mulder82/TNDisplay/blob/main/_media/nextion/icons/70/23.png) | ![Screenshot](https://github.com/mulder82/TNDisplay/blob/main/_media/nextion/icons/70/24.png) | ![Screenshot](https://github.com/mulder82/TNDisplay/blob/main/_media/nextion/icons/70/25.png) | ![Screenshot](https://github.com/mulder82/TNDisplay/blob/main/_media/nextion/icons/70/26.png) | ![Screenshot](https://github.com/mulder82/TNDisplay/blob/main/_media/nextion/icons/70/27.png)

28 | 29 | 30 | 31 | 32 | 33 | 34 | 35 | 36 | 37
-- | -- | -- | -- | -- | -- | -- | -- | -- | --
![Screenshot](https://github.com/mulder82/TNDisplay/blob/main/_media/nextion/icons/70/28.png) | ![Screenshot](https://github.com/mulder82/TNDisplay/blob/main/_media/nextion/icons/70/29.png) | ![Screenshot](https://github.com/mulder82/TNDisplay/blob/main/_media/nextion/icons/70/30.png) | ![Screenshot](https://github.com/mulder82/TNDisplay/blob/main/_media/nextion/icons/70/31.png) | ![Screenshot](https://github.com/mulder82/TNDisplay/blob/main/_media/nextion/icons/70/32.png) | ![Screenshot](https://github.com/mulder82/TNDisplay/blob/main/_media/nextion/icons/70/33.png) | ![Screenshot](https://github.com/mulder82/TNDisplay/blob/main/_media/nextion/icons/70/34.png) | ![Screenshot](https://github.com/mulder82/TNDisplay/blob/main/_media/nextion/icons/70/35.png) | ![Screenshot](https://github.com/mulder82/TNDisplay/blob/main/_media/nextion/icons/70/36.png) | ![Screenshot](https://github.com/mulder82/TNDisplay/blob/main/_media/nextion/icons/70/37.png)

38 | 39 | 40 | 41 | 42 | 43 | 44 | 45 | 46 | 47
-- | -- | -- | -- | -- | -- | -- | -- | -- | --
![Screenshot](https://github.com/mulder82/TNDisplay/blob/main/_media/nextion/icons/70/38.png) | ![Screenshot](https://github.com/mulder82/TNDisplay/blob/main/_media/nextion/icons/70/39.png) | ![Screenshot](https://github.com/mulder82/TNDisplay/blob/main/_media/nextion/icons/70/40.png) | ![Screenshot](https://github.com/mulder82/TNDisplay/blob/main/_media/nextion/icons/70/41.png) | ![Screenshot](https://github.com/mulder82/TNDisplay/blob/main/_media/nextion/icons/70/42.png) | ![Screenshot](https://github.com/mulder82/TNDisplay/blob/main/_media/nextion/icons/70/43.png) | ![Screenshot](https://github.com/mulder82/TNDisplay/blob/main/_media/nextion/icons/70/44.png) | ![Screenshot](https://github.com/mulder82/TNDisplay/blob/main/_media/nextion/icons/70/45.png) | ![Screenshot](https://github.com/mulder82/TNDisplay/blob/main/_media/nextion/icons/70/46.png) | ![Screenshot](https://github.com/mulder82/TNDisplay/blob/main/_media/nextion/icons/70/47.png)

48 | 49 | 50 | 51 | 52 | 53 | 54 | 55 | 56 | 57
-- | -- | -- | -- | -- | -- | -- | -- | -- | --
![Screenshot](https://github.com/mulder82/TNDisplay/blob/main/_media/nextion/icons/70/48.png) | ![Screenshot](https://github.com/mulder82/TNDisplay/blob/main/_media/nextion/icons/70/49.png) | ![Screenshot](https://github.com/mulder82/TNDisplay/blob/main/_media/nextion/icons/70/50.png) | ![Screenshot](https://github.com/mulder82/TNDisplay/blob/main/_media/nextion/icons/70/51.png) | ![Screenshot](https://github.com/mulder82/TNDisplay/blob/main/_media/nextion/icons/70/52.png) | ![Screenshot](https://github.com/mulder82/TNDisplay/blob/main/_media/nextion/icons/70/53.png) | ![Screenshot](https://github.com/mulder82/TNDisplay/blob/main/_media/nextion/icons/70/54.png) | ![Screenshot](https://github.com/mulder82/TNDisplay/blob/main/_media/nextion/icons/70/55.png) | ![Screenshot](https://github.com/mulder82/TNDisplay/blob/main/_media/nextion/icons/70/56.png) | ![Screenshot](https://github.com/mulder82/TNDisplay/blob/main/_media/nextion/icons/70/57.jpg)

58 | 59 | 60 | 61 | 62 | 63 | 64 | 65 | 70 | 71
-- | -- | -- | -- | -- | -- | -- | -- | -- | --
![Screenshot](https://github.com/mulder82/TNDisplay/blob/main/_media/nextion/icons/70/58.jpg) | ![Screenshot](https://github.com/mulder82/TNDisplay/blob/main/_media/nextion/icons/70/59.jpg) | ![Screenshot](https://github.com/mulder82/TNDisplay/blob/main/_media/nextion/icons/70/60.jpg) | ![Screenshot](https://github.com/mulder82/TNDisplay/blob/main/_media/nextion/icons/70/61.jpg) | ![Screenshot](https://github.com/mulder82/TNDisplay/blob/main/_media/nextion/icons/70/62.jpg) | ![Screenshot](https://github.com/mulder82/TNDisplay/blob/main/_media/nextion/icons/70/63.jpg) | ![Screenshot](https://github.com/mulder82/TNDisplay/blob/main/_media/nextion/icons/70/64.png) | ![Screenshot](https://github.com/mulder82/TNDisplay/blob/main/_media/nextion/icons/70/65.jpg) | ![Screenshot](https://github.com/mulder82/TNDisplay/blob/main/_media/nextion/icons/70/70.png) | ![Screenshot](https://github.com/mulder82/TNDisplay/blob/main/_media/nextion/icons/70/71.png)

72 | 73 | 85 
-- | -- | -- 
![Screenshot](https://github.com/mulder82/TNDisplay/blob/main/_media/nextion/icons/70/72.png) | ![Screenshot](https://github.com/mulder82/TNDisplay/blob/main/_media/nextion/icons/70/73.png) | ![Screenshot](https://github.com/mulder82/TNDisplay/blob/main/_media/nextion/icons/70/85.jpg)
