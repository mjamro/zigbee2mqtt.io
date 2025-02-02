---
title: "Xiaomi WXCJKG12LM control via MQTT"
description: "Integrate your Xiaomi WXCJKG12LM via Zigbee2MQTT with whatever smart home
 infrastructure you are using without the vendors bridge or gateway."
---

*To contribute to this page, edit the following
[file](https://github.com/Koenkk/zigbee2mqtt.io/blob/master/docs/devices/WXCJKG12LM.md)*

# Xiaomi WXCJKG12LM

| Model | WXCJKG12LM  |
| Vendor  | Xiaomi  |
| Description | Aqara Opple switch 2 bands |
| Supports | action |
| Picture | ![Xiaomi WXCJKG12LM](../images/devices/WXCJKG12LM.jpg) |

## Notes


### Binding
By default the switch is bound to the coordinator but this device can also be used to directly control other lights and switches in the network.

First unbind it from the coordinator, then you can bind it to any other device or group. (see https://www.zigbee2mqtt.io/information/binding.html )

Now change the operation mode of the device, by default it is in `event` mode, but when binding we need to change it to `command` mode.
To do this send to `zigbee2mqtt/FRIENDLY_NAME/set` payload `{"operation_mode": "command"}`, right before doing this make sure to wakeup the device.

As the device is sleeping by default, you need to wake it up after sending the bind/unbind command by pressing the reset button once.

Note that the WXCJKG12LM can only be bound to one device at a time.

When bound to a lamp, the behavior is as follows (for WXCJKG12LM Aqara Opple switch 2 band). 
- up left click: turn off
- up right click: turn on
- down left click: light dim down (by steps of 33%)
- down right click: light dim up (by steps of 33%)
- down left double click: warm white
- down right double click: cold white


## Manual Home Assistant configuration
Although Home Assistant integration through [MQTT discovery](../integration/home_assistant) is preferred,
manual integration is possible with the following configuration:


{% raw %}
```yaml
sensor:
  - platform: "mqtt"
    state_topic: "zigbee2mqtt/<FRIENDLY_NAME>"
    availability_topic: "zigbee2mqtt/bridge/state"
    icon: "mdi:gesture-double-tap"
    value_template: "{{ value_json.action }}"

sensor:
  - platform: "mqtt"
    state_topic: "zigbee2mqtt/<FRIENDLY_NAME>"
    availability_topic: "zigbee2mqtt/bridge/state"
    unit_of_measurement: "%"
    device_class: "battery"
    value_template: "{{ value_json.battery }}"

sensor:
  - platform: "mqtt"
    state_topic: "zigbee2mqtt/<FRIENDLY_NAME>"
    availability_topic: "zigbee2mqtt/bridge/state"
    icon: "mdi:signal"
    unit_of_measurement: "lqi"
    value_template: "{{ value_json.linkquality }}"
```
{% endraw %}


