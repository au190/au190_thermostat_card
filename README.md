# Lovelace custom card for Thermostat

This thermostat card is for Home Assistant Lovelace UI. 
The aim was good loking card and not set unintentionally by scrolling the screen.
https://github.com/au190/au190_bkk_stop

#### Installation
The easiest way to install it is through [HACS (Home Assistant Community Store)](https://custom-components.github.io/hacs/) search for the card in Plugins section.<br />
If you are not using HACS, you may download the configuration and put it into $homeassistant_config_dir/www/community/<br />


### TODO
- [ ] Settings can make on the default config.
- [ ] Allow changing of Opration mode on the default config.
- [ ] Automation for climate was writen in Node-red.
- [ ] ⚠️ Dual mode not tested.

*** How to set the GUI

| Operation | Preset | Color | Icon
| ---- | ---- | ------- | -----------
| Off |  | black |  
| Auto | On | Orange | auto
|   | Idle | Grey | auto
| Heat | On | Orange | heat 
|   | Idle | Grey | heat
| Cool | On | Blue | coll 
|   | Idle | Grey | coll
| Dry | On | Yellow | dry 
|   | Idle | Grey | dry
| Fan Only | On | Wgrey | fan olny 
|   | Idle | Grey | fan olny 


**Options**

| Name | Type | Default | Description
| ---- | ---- | ------- | -----------
| type | string | **Required** | `custom:au190-thermostat-card`
| entity | string | **Required** | The entity id of climate entity. Example: `climate.hvac`
| title | string | optional | Card title
| no_card | boolean | false | Set to true to avoid the card background and use the custom element in picture-elements.
| small_i | boolean | false | Set to true if you have 2 climate in one card. Default 1 big card. (Must clear browser cache after chageing this value)
| step | number | 0.5 | The step to use when increasing or decreasing temperature
| highlight_tap | boolean | false | Show the tap area highlight when changing temperature settings
| chevron_size | number | 50 | Size of chevrons for temperature adjutment
| pending | number | 3 | Seconds to wait in control mode until state changes are sent back to the server
| idle_zone | number | 2 | Degrees of minimum difference between set points when thermostat supports both heating and cooling
| ambient_temperature | string | optional | An entity id of a sensor to use as `ambient_temperature` instead of the one provided by the thermostat



**Example**
Lovelace UI:<br />
<img src='https://raw.githubusercontent.com/au190/au190_thermostat_card/master/1.png'/>


#### yaml configuraton

```yaml
climate:

  - platform: mqtt
    name: Bed room
    #availability_topic: "bedroom/ac/availability/get"
    
    current_temperature_topic: "tele/s_6/CALC"
    current_temperature_template: "{{ value_json.BMP280.Temperature }}"
    temperature_command_topic: "bedroom/ac/temperature/set"

    power_command_topic: "bedroom/ac/power/set"
    
    mode_command_topic: "bedroom/ac/mode/set"
    #mode_state_topic: "bedroom/ac/mode/get"

    fan_mode_command_topic: "bedroom/ac/fan/set"
    #fan_mode_state_topic: "bedroom/ac/fan/get"
    
    swing_mode_command_topic: "bedroom/ac/swing/set"
    #swing_mode_state_topic: "bedroom/ac/swing/get"
    
    hold_command_topic: "bedroom/ac/hold/set"
    #hold_state_topic: "bedroom/ac/hold/get"
    
    initial: 5
    retain: true
    min_temp: 5
    max_temp: 30
    temp_step: 0.5
    precision: 0.1
    modes:
      - "auto"
      - "off"
      - "heat"
      #- "cool"
      #- "fan_only"
      #- "dry"
    swing_modes:
      - "on"
      - "off"
    fan_modes:
      - "high"
      - "medium"
      - "low"
      - "auto"
    hold_modes:
      - "On"
      - "Idle"


  - platform: mqtt
    name: Living room
    #availability_topic: "living/ac/availability/get"
    
    current_temperature_topic: "tele/s_3/CALC"
    current_temperature_template: "{{ value_json.BMP280.Temperature }}"
    temperature_command_topic: "living/ac/temperature/set"

    power_command_topic: "living/ac/power/set"
    
    mode_command_topic: "living/ac/mode/set"
    #mode_state_topic: "living/ac/mode/get"

    fan_mode_command_topic: "living/ac/fan/set"
    #fan_mode_state_topic: "living/ac/fan/get"
    
    swing_mode_command_topic: "living/ac/swing/set"
    #swing_mode_state_topic: "living/ac/swing/get"
    
    hold_command_topic: "living/ac/hold/set"
    #hold_state_topic: "living/ac/hold/get"
    
    initial: 5
    retain: true
    min_temp: 5
    max_temp: 30
    temp_step: 0.5
    precision: 0.1
    modes:
      - "auto"
      - "off"
      - "heat"
      - "cool"
      - "fan_only"
      - "dry"
    swing_modes:
      - "on"
      - "off"
    fan_modes:
      - "high"
      - "medium"
      - "low"
      - "auto"
    hold_modes:
      - "On"
      - "Idle"


```


#### Lovelace UI configuration
Add the following lines to your ui-lovelace.yaml:


```
resources:

  - type: module
    url: /local/community/au190_thermostat_card/au190_thermostat_card.js
    
cards:
  - ambient_temperature: sensor.living_room_temp
    entity: climate.living_room
    small_i: true
    title: Living room
    type: 'custom:au190-thermostat-card'
  - ambient_temperature: sensor.bed_room_temp
    entity: climate.bed_room
    small_i: true
    title: Bed room
    type: 'custom:au190-thermostat-card'
type: horizontal-stack



cards:
  - ambient_temperature: sensor.bed_room_temp
    chevron_size: 50
    entity: climate.bed_room
    highlight_tap: false
    no_card: false
    small_i: true
    step: 1
    title: Bed room
    type: 'custom:au190-thermostat-card'
  - ambient_temperature: sensor.living_room_temp
    chevron_size: 50
    entity: climate.living_room
    highlight_tap: false
    no_card: false
    small_i: true
    step: 1
    title: Living room
    type: 'custom:au190-thermostat-card'
type: horizontal-stack



cards:
  - ambient_temperature: sensor.bed_room_temp
    entity: climate.bed_room
    title: Bed Room
    type: 'custom:au190-thermostat-card'
type: horizontal-stack
```



## Credits
Inspired by: https://github.com/ciotlosm/custom-lovelace/tree/master/thermostat-card