# # Lovelace custom card for Thermostat

A simple thermostat implemented in CSS based on <a href="https://codepen.io/dalhundal/pen/KpabZB/">Nest Thermostat Control</a> by Dal Hundal
 (<a href="https://codepen.io/dalhundal">@dalhundal</a>) on <a href="https://codepen.io">CodePen</a>

![thermostat](https://user-images.githubusercontent.com/7738048/42817026-7972be8e-89d5-11e8-994f-e5f556fb46fc.png)

### TODO
There are many things still missing, but I'll add below those that I know of
- [ ] Allow canceling of schedules for thermostats like Ecobee
- [ ] Allow settings Away mode
- [ ] Allow changing of Opration mode
- [ ] Add support for multiple entities for different functions (zwave thermostats hot/cold, tado away mode, etc)
- [ ] Title scaling

**Options**

| Name | Type | Default | Description
| ---- | ---- | ------- | -----------
| type | string | **Required** | `custom:thermostat-card`
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

```yaml
resources:
  - url: /local/custom-lovelace/thermostat-card/thermostat-card.js?v=1
    type: module
name: My Awesome Home
views:
  - title: Home
    cards:
      - type: custom:thermostat-card
        title: Bedroom
        entity: climate.ecobee
```

**Example with custom hvac_states**

```yaml
resources:
  - url: /local/custom-lovelace/thermostat-card/thermostat-card.js?v=1
    type: module
name: My Awesome Home
views:
  - title: Home
    cards:
      - type: custom:thermostat-card
        title: Bedroom
        entity: climate.hvac
        chevron_size: 100
        hvac:
          states:
            'Off': 'off'
            'Cooling': 'cool'
            'Heating': 'heat'
          attribute: operation_mode
```

Example with external ambient sensor
```yaml
- type: custom:thermostat-card
  title: Bedroom
  entity: climate.ecobee
  ambient_temperature: sensor.bedroom_temperature
```

⚠️ Make sure you set type to `module` when including the resource file.

This Lovelace custom card displays Budapest Public Transportation (BKK)
line information departing in the near future from a configurable stop.<p>
This custom card depends on the BKK Stop Information custom component that you may find at
https://github.com/au190/au190_bkk_stop


#### Installation
The easiest way to install it is through [HACS (Home Assistant Community Store)](https://custom-components.github.io/hacs/),
search for <i>bkk</i> and select BKK Stop Card from Plugins.<br />
If you are not using HACS, you may download bkk_stop_card.js and put it into $homeassistant_config_dir/www.<br />

#### Lovelace UI configuration
Add the following lines to your ui-lovelace.yaml (entity should be the sensor of bkk_stop platform you defined):
```
resources:
  - {type: module, url: '/www/community/au190_bkk_stop_card/au190_bkk_stop_card.js '}

cards:
  - entity: sensor.99_home_city
    type: 'custom:bkk-stop-card'
  - entity: sensor.99_vajdapeter_home
    type: 'custom:bkk-stop-card'
  - entity: sensor.99_blaha_home
    type: 'custom:bkk-stop-card'
  - entity: sensor.99_tess_home
    type: 'custom:bkk-stop-card'
  - entity: sensor.23_boraros_home
    type: 'custom:bkk-stop-card'
  - entity: sensor.23_home_city
    type: 'custom:bkk-stop-card'
type: vertical-stack
```

Lovelace UI:<br />
<img src='https://raw.githubusercontent.com/au190/au190_bkk_stop_card/master/bkk_lovelace.png'/>

## Credits
[@silasb](https://github.com/silasb)
[@ciotlosm](https://github.com/ciotlosm)
Original: https://github.com/ciotlosm/custom-lovelace/tree/master/thermostat-card