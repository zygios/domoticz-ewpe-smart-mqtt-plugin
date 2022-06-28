# EwpeSmart - Domoticz Python Plugin
Python plugin for Domoticz to control ewpe-smart powered air conditioners which can be controled via WiFi using [EWPE Smart app](https://play.google.com/store/apps/details?id=com.gree.ewpesmart)

![gree-plugin](https://user-images.githubusercontent.com/2734836/49314936-aeffd700-f4f4-11e8-96a7-11310dac543c.PNG)

## Prerequisites

Setup [ewpe-smart-mqtt](https://github.com/stas-demydiuk/ewpe-smart-mqtt) bridge

##EWPE-SMART-MQTT autorun

1. cd /etc/systemd/system
2. sudo nano ewpe-smart-mqtt.service

Write next text to file:
```
[Unit]
Description=EWPE Smart MQTT
After=network.target
StartLimitIntervalSec=0
[Service]
Type=simple
WorkingDirectory=/home/ewpe-smart-mqtt
ExecStart=node --expose-gc /home/ewpe-smart-mqtt/index.js
Restart=always
RestartSec=1
StandardOutput=syslog
StandardError=syslog
SyslogIdentifier=ewpe-smart-mqtt
User=root
Group=root
Environment=NODE_ENV=production

[Install]
WantedBy=multi-user.target
```
3. sudo chmod 777 ewpe-smart-mqtt.service
4. sudo systemctl enable ewpe-smart-mqtt.service

## Installation

1. Clone repository into your domoticz plugins folder
```
cd domoticz/plugins
git clone https://github.com/stas-demydiuk/domoticz-ewpe-smart-mqtt-plugin.git ewpe-smart-mqtt
```
2. Restart domoticz
3. Go to "Hardware" page and add new item with type "EwpeSmart Air Conditioners via MQTT"
4. Set your MQTT server address and port to plugin settings

## Plugin update

1. Stop domoticz
2. Go to plugin folder and pull new version
```
cd domoticz/plugins/ewpe-smart-mqtt
git pull
```
3. Start domoticz

## Supported devices
All devices which can be controlled via EWPE Smart or Gree+ app should be supported, including:

- Gree: Smart, U-CROWN series
- Cooper&Hunter: Supreme, Vip Inverter, ICY II, Arctic, Alpha, Alpha NG, Veritas, Veritas NG series
- EcoAir X series
