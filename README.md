# EGLO 99099 HA Blueprint

Home Assistant automation blueprint for the **EGLO 99099 / ERCU_3groups_Zm** remote when used through Zigbee2MQTT.

It lets you independently assign Home Assistant actions to the supported MQTT actions for groups 1, 2 and 3.

## Install

Import the blueprint into Home Assistant using:

`https://raw.githubusercontent.com/fct-sk/Eglo-99099-HA-blueprint/main/blueprints/automation/eglo_99099_button_mapper.yaml`

Then go to **Settings → Automations & scenes → Blueprints** and create an automation from the blueprint.

## Defaults

- Zigbee2MQTT base topic: `zigbee2mqtt1`
- Remote friendly name: `EgloRemote`
- MQTT topic: `zigbee2mqtt1/EgloRemote`

Both values can be changed when creating the automation.

## Supported actions

`on`, `off`, `red`, `red_long`, `refresh`, `refresh_long`, `refresh_colored`, `refresh_colored_long`, `blue`, `blue_long`, `green`, `green_long`, `brightness_step_up`, `brightness_step_down`, `brightness_move_to_level`, `color_temperature_step_up`, `color_temperature_step_down`, `color_temperature_move`, `recall_1`, `recall_1_long`, `recall_2`, `recall_2_long`.

The physical group-selection / pairing buttons are not mapped because they are used by the remote for direct pairing with EGLO lights rather than being exposed as ordinary network actions.

## Groups

The MQTT payload contains `action_group` values **1**, **2**, or **3**. The blueprint routes each action to the corresponding Group 1, Group 2, or Group 3 configuration.

## Requirements

- Home Assistant 2024.6.0 or newer.
- MQTT integration configured.
- Zigbee2MQTT publishing the EGLO remote messages.

## Device documentation

https://www.zigbee2mqtt.io/devices/99099.html
