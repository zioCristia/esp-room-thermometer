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

![alt text](/images/IMG_4552.jpg)
![alt text](/images/IMG_4554.jpg)

## Hardware
The module is composed by:
* esp8266-01
* dht11 temperature and umidity sensor
* hlk-pm03 as ac-dc transformer
* 4.7k ohm resistor
* 50uF capacitor

I have also used a JST connector to bring 220v to the board.
The esp is programmed before the insertion in the module thanks to a usb adapter, the following updates can be done over the air thanks to the EspHome software.

I didn't want batteries to power the module so you don't have the bother of changing them and making sure they are charged, plus I think in the long run changing a battery every year or so is not convenient.
However if that is more suitable for you there will be no problmes to add a battery holder and use a 3.3V battery.

I know that DHT11 is not a very reliable temperature and umidity sensor but for the purpose of this project is more than sufficient.

For a complete list of parts with some links: https://docs.google.com/spreadsheets/d/1-pkWVYFf2BbrVPfpay5KMb0pS1-IxxCx1xM6d1OcC2A/edit#gid=0

## Software
The software used is EspHome in order to integrate the sensors with my HomeAssistant server but you may as well use another software to your liking.

After adding your new esp device in EspHome, as a generic esp8266 board, the only thing to add in the code is the following:
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

You can add some [filters](https://esphome.io/components/sensor/index.html#sensor-filters) for calibrating dht, this should be done by comparison with a reliable thermometer.

Check the [complete .yaml file](/room-temperature.yaml.example) if you need an example ready to use for your EspHome device.

## Pcb
The design of the pcb has been made with Eagle. The various components were added thanks to libraries found on the internet.
For semplicity reasons all the components are throgh hole and the esp is inserted thanks to female socket header connectors.

In one side of the pcb there are esp and dht11 and in the other hlk and a jst connector for power supply. The intention was to have all soldered on the board but the heat released by the hlk and the esp compromised the reading of temperature and umidity values. For this reason dht sensor is istalled thanks to 10cm cables soldered to the pcb. Some 3 way jst connector could be use to have a nicer design. 

![alt text](/images/schematics.png)
![alt text](/images/board-v1.png)

The second version of the pcb allows to have larger distance between dht11 and other components and allows to have all soldered in the pcb. If you have more space available inside your switches box, it's prefereable to use v2 (but it is not tested yet).

![alt text](/images/board-v2.png)

If you prefer to use battery power you can place a battery holder where there is the hlk and esily make a sensor similar to the ones ready to use with a lower overall cost.

## 3D printed enclouser
The pourposes of the 3d enclouser are: 
- to mantain in a fix position the dht sensor
- to allow proper measurements of the room temperature thanks to openings 
- to be able to place the module in a hidden way next to the power switches.

In my home we have btcino switches, so a similar design was needed.

To be continued...
