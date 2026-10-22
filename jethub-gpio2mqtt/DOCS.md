# JetHome peripheral exposer

Expose [JetHome JetHub](https://jethome.ru) GPIO resources (relays, inputs, LEDs) to
Home Assistant via [gpio2mqtt](https://github.com/jethome-iot/gpio2mqtt) with
autodiscovery support.

This is the next-generation addon based on the gpio2mqtt daemon. Compared to the
legacy [jethub-mqtt-io](https://github.com/jethome-hassio-addons/addon-jethub-mqtt-io)
addon, it uses the new MQTT topic structure by default, which changes the entity IDs
created in Home Assistant.

**Note:** This addon checks at startup that the legacy `jethub-mqtt-io` addon
is not running: both claim the same GPIO lines. If it is running, this addon
stops with an explanation in the log and ends in the error state — stop and
disable `jethub-mqtt-io` first.

**Watchdog:** keep the Supervisor watchdog toggle OFF for this addon. An
intentional startup refusal exits with a non-zero code by design; the
watchdog would retry the start a few times before giving up, which only
adds noise.

## Supported Devices

| Model                | Description                                                           |
| -------------------- | --------------------------------------------------------------------- |
| JetHub H1 (J80)      | JetHome ARM controller                                                |
| JetHub D1/D1+ (J100) | JetHome ARM controller with 4 inputs, 3 relays, status LED            |
| JetHub D2 (J200)     | JetHome ARM controller with 3 inputs, 2 relays, status LED, UXM slots |
| JetHub D3 (J310)     | JetHome modular ARM controller (S905Y5) with 4 UXM slots              |

## Configuration

**Note**: _Remember to restart the add-on when the configuration is changed._

### Simple Configuration

With auto-detection and MQTT auto-discovery from Home Assistant:

```yaml
log_level: info
jethub_model: auto
use_module_config: false
mqtt:
  client_id: jethub-gpio2mqtt
  topic_prefix: jethub-gpio2mqtt
```

### Advanced Configuration

With manual MQTT settings:

```yaml
log_level: info
jethub_model: auto
use_module_config: true
mqtt:
  host: 192.168.1.100
  port: 1883
  user: my_user
  password: my_password
  client_id: jethub-gpio2mqtt
  topic_prefix: jethub-gpio2mqtt
```

### Custom Configuration

You can provide a complete custom gpio2mqtt configuration in the `custom_config` field.
MQTT settings from the addon options will still be applied on top of your custom config.
This also allows switching to the Wirenboard MQTT convention
(`options.convention: wirenboard`) or exposing custom pins.

## Options

### Option: `log_level`

Log level for the application.

**Values**: `trace`, `debug`, `info`, `warning`, `error`
**Default**: `info`

### Option: `jethub_model`

JetHub model selection.

**Values**:

- `auto` - Auto-detect JetHub model from device tree (HAOS only)
- `jethub-h1` - JetHome JetHub H1 (J80)
- `jethub-d1` - JetHome JetHub D1/D1+ (J100)
- `jethub-d2` - JetHome JetHub D2 (J200)
- `jethub-d3` - JetHome JetHub D3 (J310)
- `manual` - Use custom configuration (requires `custom_config`)

**Default**: `auto`

### Option: `use_module_config`

Use module configuration variant that includes additional GPIO pins
for ZigBee/UXM module control (BOOT, RESET pins).

**Default**: `false`

**Note**: The JetHub D3 base configuration already includes the UXM control
lines, so this option has no additional effect on D3 (the base config is used).

### Option: `restore_mode`

Startup behavior of the outputs (relays, LEDs, module control lines) after a
restart or power cycle:

- `restore` - restore the last state from the MQTT retained message; fall
  back to the built-in default when no retained value exists
- `off` - never restore; switch everything OFF at startup
- `on` - never restore; switch everything ON at startup

**Default**: `restore`

This applies to every output that does not define its own `restore_mode` /
`restore_state` (e.g. outputs from a `custom_config`). Inputs are always
re-published on (re)connect, and states survive a full broker restart, so
nothing needs to be configured for them.

### Option: `custom_config`

Optional custom gpio2mqtt YAML configuration. If provided, this will be used
instead of the built-in configuration for your JetHub model.

**Default**: empty

### Group: `mqtt`

MQTT connection settings.

| Option               | Description                                           | Default            |
| -------------------- | ----------------------------------------------------- | ------------------ |
| `mqtt.host`          | MQTT server host (leave blank for auto-discovery)     | auto               |
| `mqtt.port`          | MQTT server port (leave blank for auto-discovery)     | auto               |
| `mqtt.user`          | MQTT server user (leave blank for auto-discovery)     | auto               |
| `mqtt.password`      | MQTT server password (leave blank for auto-discovery) | auto               |
| `mqtt.client_id`     | MQTT client ID                                        | `jethub-gpio2mqtt` |
| `mqtt.topic_prefix`  | MQTT topic prefix for state/command topics            | `jethub-gpio2mqtt` |
| `mqtt.legacy_mqttio` | Use legacy mqtt-io entity naming (see below)          | `false`            |
| `mqtt.keepalive`     | MQTT keepalive interval (seconds)                     | `60`               |
| `mqtt.qos`           | MQTT QoS level (0, 1, or 2)                           | `1`                |

### Option: `mqtt.legacy_mqttio`

Controls how Home Assistant discovery entities are named:

- `false` (default) — gpio2mqtt format. Discovery topics use the device
  identifier as node_id: `homeassistant/{component}/{device_id}/{object_id}/config`.
  Entities belong to a proper device in Home Assistant.
- `true` — legacy mqtt-io compatible format. Discovery topics use the MQTT
  client_id: `homeassistant/{component}/{client_id}/{name}/config`.
  This reproduces the entity IDs created by the old mqtt-io / jethub-mqtt-io
  addon, so existing automations and dashboards keep working.

State and command topics are not affected by this option (see below).

## MQTT Topics

### State topics (both modes)

```
{topic_prefix}/input/{name}       # Input state (ON/OFF)
{topic_prefix}/output/{name}      # Output state (ON/OFF)
{topic_prefix}/output/{name}/set  # Output command
{topic_prefix}/status             # Device availability (online/offline)
```

### Home Assistant Discovery

The addon automatically registers devices and entities in Home Assistant
via MQTT discovery. No manual configuration is required.

### Wirenboard convention

Via `custom_config` the daemon can also publish in the Wirenboard convention
(`/devices/{device}/controls/{name}`). See the
[gpio2mqtt documentation](https://github.com/jethome-iot/gpio2mqtt) for details.

## Migrating from the jethub-mqtt-io addon

1. Install this addon (it can coexist with the old one while both are stopped).
2. Configure it (model, MQTT — defaults usually suffice).
3. **Stop and disable** the `jethub-mqtt-io` addon — the startup check of this
   addon will tell you if it is still in the way.
4. Start this addon. New entities will appear, grouped under a JetHub device.
5. Update your automations and dashboards to the new entity IDs.

If you need the old entity IDs back temporarily, set `mqtt.legacy_mqttio` to `true`.

## Exposed GPIO Resources

### JetHub D1/D1+ (Basic)

| Resource            | Type   | Description        |
| ------------------- | ------ | ------------------ |
| jethub_front_button | Input  | Front panel button |
| jethub_input_1..4   | Input  | Digital inputs     |
| stat_led_red        | Output | Status LED (red)   |
| stat_led_green      | Output | Status LED (green) |
| jethub_relay_1..3   | Output | Relays             |

### JetHub D1/D1+ (Module)

Includes all basic resources plus:

| Resource     | Type   | Description             |
| ------------ | ------ | ----------------------- |
| zigbee_boot  | Output | ZigBee module BOOT pin  |
| zigbee_reset | Output | ZigBee module RESET pin |

### JetHub D2 (Basic)

| Resource           | Type   | Description        |
| ------------------ | ------ | ------------------ |
| jethub_user_button | Input  | Front panel button |
| jethub_input_1..3  | Input  | Digital inputs     |
| jethub_relay_1..2  | Output | Relays             |

### JetHub D2 (Module)

Includes all basic resources plus UXM slot control pins:

| Resource   | Type   | Description          |
| ---------- | ------ | -------------------- |
| uxm1_reset | Output | UXM slot 1 RESET pin |
| uxm1_boot  | Output | UXM slot 1 BOOT pin  |
| uxm2_reset | Output | UXM slot 2 RESET pin |
| uxm2_boot  | Output | UXM slot 2 BOOT pin  |

### JetHub D3 (J310)

The D3 is a modular controller: the base board has no relays or digital
inputs — I/O functions are provided by the plugged UXM modules. The addon
exposes the UXM module control lines, which live on the TCA6408A I2C port
expander (the chip is resolved automatically at startup):

| Resource   | Type   | Description               |
| ---------- | ------ | ------------------------- |
| uxm1_reset | Output | UXM slot 1 RESET (nRESET) |
| uxm1_mode  | Output | UXM slot 1 MODE (nMODE)   |
| uxm2_reset | Output | UXM slot 2 RESET          |
| uxm2_mode  | Output | UXM slot 2 MODE           |
| uxm3_reset | Output | UXM slot 3 RESET          |
| uxm3_mode  | Output | UXM slot 3 MODE           |
| uxm4_reset | Output | UXM slot 4 RESET          |
| uxm4_mode  | Output | UXM slot 4 MODE           |

Notes:

- The RGB status LED is managed by the kernel `gpio-leds` driver and is
  deliberately not exposed by this addon.
- RESET/MODE switches are inverted (active-low): switch OFF = module running.

### JetHub H1 (Basic)

| Resource | Type   | Description |
| -------- | ------ | ----------- |
| stat_led | Output | Status LED  |

### JetHub H1 (Module)

Includes all basic resources plus:

| Resource      | Type   | Description             |
| ------------- | ------ | ----------------------- |
| zigbee_reset  | Output | ZigBee module RESET pin |
| zigbee_boot   | Output | ZigBee module BOOT pin  |
| module2_reset | Output | Module-2 slot RESET pin |
| module2_boot  | Output | Module-2 slot BOOT pin  |

## Troubleshooting

### GPIO Access Issues

If you experience GPIO access issues, ensure that:

1. The addon has GPIO access enabled (should be automatic)
2. The legacy `jethub-mqtt-io` addon is stopped (GPIO lines conflict)
3. No other service is using the same GPIO pins via sysfs

The addon automatically unexports GPIO pins from sysfs before starting.

### MQTT Connection Issues

If MQTT auto-discovery fails:

1. Ensure the Mosquitto broker addon is installed and running
2. Try specifying MQTT settings manually in the addon configuration

### Model Detection Issues

If auto-detection fails:

1. Check addon logs for detection errors
2. Manually specify your JetHub model in the configuration

## Support

- [GitHub Issues](https://github.com/jethome-hassio-addons/addon-jethub-gpio2mqtt/issues)
- [JetHome Website](https://jethome.ru)
