# EGLO 99099 HA Blueprint

Home Assistant blueprint for the **EGLO 99099 / ERCU_3groups_Zm** remote when used through Zigbee2MQTT.

The blueprint maps the remote's MQTT `action` together with `action_group` 1, 2, or 3 to configurable Home Assistant actions.

## Import

Use this Raw URL in **Settings → Automations & scenes → Blueprints → Import Blueprint**:

`https://raw.githubusercontent.com/fct-sk/Eglo-99099-HA-blueprint/main/blueprints/automation/eglo_99099_button_mapper.yaml`

Default MQTT topic:

`zigbee2mqtt1/EgloRemote`

The topic can be changed when creating the automation.

## How the remote is represented

On this EGLO remote, buttons **1 / 2 / 3** select the active group. Zigbee2MQTT does not publish the group-selection press itself as a separate action; instead, the following command is published with the selected group in `action_group`.

Examples:

```json
{"action":"on","action_group":1}
{"action":"brightness_step_up","action_group":2}
{"action":"recall_1","action_group":3}
```

The blueprint therefore does not need separate triggers for buttons 1/2/3. It matches `action` + `action_group`.

Release messages where `action` is missing/null are ignored.

## Verified action map

| Function | Zigbee2MQTT action |
|---|---|
| ON | `on` |
| OFF | `off` |
| Red | `red` |
| Red — long press | `red_long` |
| Green | `green` |
| Green — long press | `green_long` |
| Blue | `blue` |
| Blue — long press | `blue_long` |
| Refresh / white | `refresh` |
| Refresh / white — long press | `refresh_long` |
| Colored refresh | `refresh_colored` |
| Colored refresh — long press | `refresh_colored_long` |
| Brightness + | `brightness_step_up` |
| Brightness − | `brightness_step_down` |
| Brightness — set level | `brightness_move_to_level` |
| Color temperature + | `color_temperature_step_up` |
| Color temperature − | `color_temperature_step_down` |
| Color temperature — move | `color_temperature_move` |
| Favorite / Heart 1 | `recall_1` |
| Favorite / Heart 1 — long press | `recall_1_long` |
| Favorite / Heart 2 | `recall_2` |
| Favorite / Heart 2 — long press | `recall_2_long` |

For the verified EGLO 99099 payloads, the remote also exposes:

- `action_level` for `brightness_move_to_level`
- `action_color_temperature` for `color_temperature_move`
- `action_step_size` for brightness step events
- `action_color_temperature_delta` for color-temperature step events
- `action_transition_time` for move events

The current blueprint passes these events to the user-selected Home Assistant actions. The raw payload values remain available in the automation trace/template context as `trigger.payload_json`.

## Group behavior

Once a group is selected on the physical remote, every supported action carries that group's number in `action_group`.

For example:

```text
2 → ON             → on + group 2
2 → large sun      → brightness_step_up + group 2
2 → heart 1        → recall_1 + group 2
```

## Requirements

- Home Assistant 2024.6.0 or newer.
- MQTT integration configured.
- Zigbee2MQTT publishing the EGLO remote messages.

## Source

Device documentation:

https://www.zigbee2mqtt.io/devices/99099.html
