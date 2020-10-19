---
title: "Lonsonho QS-Zigbee-S05-LN control via MQTT"
description: "Integrate your Lonsonho QS-Zigbee-S05-LN via Zigbee2MQTT with whatever smart home
 infrastructure you are using without the vendors bridge or gateway."
---

*To contribute to this page, edit the following
[file](https://github.com/Koenkk/zigbee2mqtt.io/blob/master/docs/devices/QS-Zigbee-S05-LN.md)*

# Lonsonho QS-Zigbee-S05-LN

| Model | QS-Zigbee-S05-LN  |
| Vendor  | Lonsonho  |
| Description | 2 gang switch module with neutral wire |
| Supports | on/off |
| Picture | ![Lonsonho QS-Zigbee-S05-LN](../images/devices/QS-Zigbee-S05-LN.jpg) |

## Notes

None

## Manual Home Assistant configuration
Although Home Assistant integration through [MQTT discovery](../integration/home_assistant) is preferred,
manual integration is possible with the following configuration:


{% raw %}
```yaml
switch:
  - platform: "mqtt"
    state_topic: "zigbee2mqtt/<FRIENDLY_NAME>"
    availability_topic: "zigbee2mqtt/bridge/state"
    payload_off: "OFF"
    payload_on: "ON"
    value_template: "{{ value_json.state_l1 }}"
    command_topic: "zigbee2mqtt/<FRIENDLY_NAME>/l1/set"

sensor:
  - platform: "mqtt"
    state_topic: "zigbee2mqtt/<FRIENDLY_NAME>"
    availability_topic: "zigbee2mqtt/bridge/state"
    icon: "mdi:signal"
    unit_of_measurement: "lqi"
    value_template: "{{ value_json.linkquality }}"
```
{% endraw %}


