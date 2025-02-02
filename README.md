# MMM-EnergyMonitor

This is a module for the [MagicMirror²](https://github.com/MagicMirrorOrg/MagicMirror/).

This module visualizes current energy production and consumption of your home. It is meant to be used when you have a electric power generator (such as a photovoltaic system) and a battery (optional) installed in your home.

## About

The module has the following features:

- Show live data of power production and consumption of your home
- The module is developed to be used in _center regions_ of the MagicMirror. If you want to use it somewhere else, please feel free to submit a Pull Request.
- This module was developed as a companion to [MMM-Fronius2](https://github.com/deg0nz/MMM-Fronius2) and [MMM-VartaESS](https://github.com/deg0nz/MMM-VartaESS) to visualize their data. But other data sources are supported as well.

**Attention: This module depends on external data sources. It _cannot_ be used as standalone module. Please refer to the "Data Sources" section below!**

## Installing

This module has no external dependencies (apart from the data sources mentiones above). Just clone it:

```bash
cd modules
git clone https://github.com/deg0nz/MMM-EnergyMonitor
```

## Status

The current development status of this module is: **maintained**

This means: I'm open for feature requests, pull requests, bug reports, ...

## Screenshots

![](assets/screenshot-energy-monitor.png)

## Using the module

To use this module, add the following configuration block to the modules array in the `config/config.js` file:

```js
        {
            module: 'MMM-EnergyMonitor',
            position: 'middle_center'
        },
```

## Configuration options

_Note: You should test `size`s that work for your mirror resolution. All the other values are calculated and should scale automatically_

Please refer to [MMM-EnergyMonitor default configuration](MMM-EnergyMonitor.js) to prevent syntax errors.

| Option                                     | Description                                                                                                                                                                                                                                                                             |
| ------------------------------------------ | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `energyStorage`                            | _Optional_ Configure if you have Energy Storage System installed in your home and it should be displayed by the module<br><br>**Type:** `boolean` (yes/no) <br>Default: `true` (yes - ESS installed)                                                                                    |
| `size`                                     | _Optional_ The size of the module. Can be one of<br>- xlarge<br>- large<br>- medium<br>- small<br>- xsmall<br><br>**Type:** String<br>Default: `large` (700 pixels wide and 600 pixels high pixel)                                                                                      |
| `updateInterval`                           | _Optional_ How often should the UI be updated<br><br>**Type:** `int` (milliseconds) <br>Default: `3000` milliseconds (3 seconds)                                                                                                                                                        |
| `resetCycles`                              | _Optional_ After how many UI update cycles without new data should the values be reset to 0. _Note: `resetCycles` _ `updateInterval` musst be greater than the interval that updates the actual data!\*<br><br>**Type:** `int` (cycles) <br>Default: `3` cycles                         |
| `logNotifications`                         | _Optional_ If the module should log the data notifications/updates it receives. This value is good for debugging if the module shows weird values.<br><br>**Type:** `boolean` (on/off)<br>Default: `false` off                                                                          |
| `wattConversionOptions`                    | _Optional_ Configures if and how Watts should get converted to kW<br><br>**Type:** `object` <br>See configuration below                                                                                                                                                                 |
| `wattConversionOptions`.`enabled`          | _Optional_ Turns the feature on/off<br><br>**Type:** `boolean` (on/off)<br>Default: `true` (on)                                                                                                                                                                                         |
| `wattConversionOptions`.`threshold`        | _Optional_ At which value should numbers be converted <br><br>**Type:** `int` (Watt) <br>Default: `1200` Watt                                                                                                                                                                           |
| `wattConversionOptions`.`numDecimalDigits` | _Optional_ To how many decimal digits should the converted value be shortened (keep this value low to prevent UI glitches) <br><br>**Type:** `int` <br>Default: `2` (example: 1.45 kW)                                                                                                  |
| `iconCssClasses`                           | _Optional_ Changes the default CSS classes of the icons. Currently, [Font Awesome free icons v5](https://fontawesome.com/v5/search) are supported. _Attention: don't forget the `fas` prefix as shown in the examples below!_<br><br>**Type:** `object` <br>See object properties below |
| `iconCssClasses`.`home`                    | _Optional_ Icon for the home<br><br>**Type:** `string` (CSS classes)<br>Default: `fas fa-home` (Home icon)                                                                                                                                                                              |
| `iconCssClasses`.`grid`                    | _Optional_ Icon for the power grid<br><br>**Type:** `string` (CSS classes) <br>Default: `fas fa-plug` (Plug icon)                                                                                                                                                                       |
| `iconCssClasses`.`energyStorage`           | _Optional_ Icon for the energy storage<br><br>**Type:** `string` (CSS classes)<br>Default: `fas fa-battery-half` (Battery half full)                                                                                                                                                    |
| `iconCssClasses`.`localPowerSource`        | _Optional_ Icon for the local power source (e.g. Power)<br><br>**Type:** `string` (CSS classes)<br>Default: `fas fa-solar-panel` (Solar panel)                                                                                                                                          |

## Data Sources

Per default, the companion modules [MMM-Fronius2](https://github.com/deg0nz/MMM-Fronius2) and [MMM-VartaESS](https://github.com/deg0nz/MMM-VartaESS) are able to send data to this module. You can use other modules as data sources for this module.

All the values are expected to be from the point of view of the corresponding system. Negative values are interpreted as _pulling energy from_ the system. Positive values are interpreted as _pushing energy into_ the system.

Other modules can send the following notifications to update data for this module:

| Notification                                    | Unit | What is updated | Interpretation                                                                                                                                                  |
| ----------------------------------------------- | ---- | --------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `MMM-EnergyMonitor_ENERGY_STORAGE_POWER_UPDATE` | Watt | Energy Storage  | **Negative** values ar interpreted as **drawing** power **from the energy storage**.<br>**Positive** values are interpreted as **charging the energy storage**. |
| `MMM-EnergyMonitor_GRID_POWER_UPDATE`           | Watt | Grid Power      | **Negative** values ar interpreted as _drawing_ power _from the grid_.<br>**Positive** values are interpreted as **feeding** back **into the grid**.            |
| `MMM-EnergyMonitor_SOLAR_POWER_UPDATE`          | Watt | Solar Power     | The currently produced solar powwer. This value must always be 0 or positive.                                                                                   |

## Special Thanks

- [MichMich](https://github.com/MichMich) for creating the MagicMirror² Project
- [hukl](http://smyck.net) for creating the [SMYCK color theme](http://color.smyck.org) on which the default colors are based

## Issues

If you find any problems, bugs or have questions, please open a [GitHub issue](https://github.com/deg0nz/MMM-EnergyMonitor/issues) in this repository.

## Disclaimer

All product and company names are trademarks™ or registered® trademarks of their respective holders. Use of them does not imply any affiliation with or endorsement by them.
