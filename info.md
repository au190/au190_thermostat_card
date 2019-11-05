# SZÉP Kártya Home Assistant custom component

Custom component for [Home Assistant](https://homeassistant.io) that tracks the balance of a card.
The state of the sensor is the sum of all sub-balances, but each sub-balance is exposed as a property.

#### Example card:
<img src='https://raw.githubusercontent.com/au190/au190_szep_kartya/master/1.png'/>


## Installation
#### Installation
1. The easiest way to install it is through [HACS (Home Assistant Community Store)](https://custom-components.github.io/hacs/) search for <i>szep_kartya</i> and select from Plugins.<br />
2. If you are not using HACS, you may download `au190_szep_kartya` from github
3. Unzip `au190_szep_kartya` and copy the `custom_components` directory inside your Home Assistant `custom_components` folder.
2. Restart Home Assistant (this installs the component's dependencies)
3. Add your config to `configuration.yaml` (see options below)
4. Restart Home Assistant again

## Configuration

``` yaml
sensor:
  - platform: au190_szep_kartya
    card_number: !secret card_number
    card_code: !secret card_code
    name: SZÉP Kártya
```

`card_number`: The last 8 digits of the card (after the `61013242` prefix)
`card_code`: "Telekód" (by default the last 3 digits of card number)
`name` (optional): Friendly name of the sensor

Added HACS support
Original: https://github.com/ofalvai/home-assistant-szep-kartya