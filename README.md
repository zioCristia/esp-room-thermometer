# Esp room thermometer
Esp8266-01 based module, 220V ac powered, for measuring room temperature for your domotic house.
Any possibility of improvement is accepted.

## Table of contenets
* [General info](#general-info)
* [Hardware](#hardware)
* [Software](#software)
* [Pcb](#pcb)
* [3D printed enclouser](#3d-printed-enclouser)

## General info
I built this module to have an inexpensive and reliable sensor in every room of my house. 
Total cost per sensor is around 5.5€ and includes all components and pcb. It does not rely on batteries but on an ac-dc transformer type HLK-PM03. 

The design is intended to minimize the dimensions and thus be able to put the sensor inside the power boxes, where there are light switches to be clear. I 3D printed a container to be able to easily insert it in the boxes type btcino and allow the sensor to effectively detect the temperature and humidity outside through some openings.

## Hardware
The module is composed by:
* esp8266-01
* dht11 temperature and umidity sensor
* hlk-pm03 as ac-dc transformer
* 4.7k ohm resistor
* 50uF capacitor

I have inserted a JST connector to bring 220v to the board
The esp is programmed before the insertion in the module thanks to a usb adapter, the following updates can be done over the air thanks to the EspHome software.

## Software
The software used is EspHome in order to integrate the sensors with my HomeAssistant server but you may well use another software to your liking.

After adding your new esp device in EspHome, as a generic esp8266 board, the only thing part to add at the code is the following:
```
sensor:
  - platform: dht
    pin: GPIO2
    temperature:
      name: "Room temperature"
    humidity:
      name: "Room umidity"
    update_interval: 60s
```

This allows us to read the values of temperature and umidity and have them as a sensor in our Home Assistant server.

## Pcb

## 3D printed enclouser
