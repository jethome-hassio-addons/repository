# JetHome peripheral exposer 1.0.0 — first stable release

Next-generation add-on built on the [gpio2mqtt](https://github.com/jethome-iot/gpio2mqtt) daemon (binary **0.2.2**), replacing the legacy `jethub-mqtt-io` add-on.

## Highlights

- **Modern MQTT discovery**: entities are grouped under a JetHub device, discovery payloads follow current Home Assistant recommendations (`origin` block, availability list, `has_entity_name`-friendly short entity names).
- **Legacy compatibility switch**: `mqtt.legacy_mqttio: true` reproduces the old mqtt-io entity IDs for a gradual migration.
- **JetHub D1/D1+ (J100), D2 (J200), D3 (J310), H1 (J80)** support out of the box; model auto-detection on HAOS.
- **JetHub D3**: UXM1–4 RESET/MODE control lines on the TCA6408A I2C port expander, gpiochip auto-resolved at startup.
- **State restore after power cycle**: `restore_mode` option (`restore` / `off` / `on`, default `restore`) — output states survive restarts via MQTT retained messages.
- **Reliable MQTT lifecycle**: everything is published strictly after ConnAck and re-published on every reconnect; HA birth message handled; input states retained.
- **Startup guard**: refuses to start while the legacy `jethub-mqtt-io` add-on is running (both claim the same GPIO lines) — with a clear, red explanation in the log.

## Migration from jethub-mqtt-io

1. Install this add-on (keep both stopped).
2. Stop & disable `jethub-mqtt-io`.
3. Start this add-on; new entities appear under a JetHub device — update automations and dashboards.

Full documentation: [DOCS.md](https://github.com/jethome-hassio-addons/addon-jethub-gpio2mqtt/blob/main/jethub-gpio2mqtt/DOCS.md)
