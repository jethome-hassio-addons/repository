# Home Assistant Add-on: JetHome peripheral exposer

[![Release][release-shield]][release] ![Project Stage][project-stage-shield] ![Project Maintenance][maintenance-shield]

## About

Expose [JetHome JetHub](https://jethome.com) resources (relays,inputs,etc..) to Home Assistant via gpio2mqtt

This addon uses the new gpio2mqtt MQTT topic structure, which changes the entity IDs
in Home Assistant compared to the legacy jethub-mqtt-io addon.
It refuses to start while the legacy jethub-mqtt-io addon is running
(both claim the same GPIO lines) — stop the legacy add-on first.

**Note**: _All used GPIOs will **disappear** from **/sys/class/gpio** during addon run_

**Warning:** The auto-detection option works only on HAOS (Home Assistant Operating System).
For Home Assistant Supervised, please select your device manually in the configuration.


## Supported devices:

### [JetHome JetHub D1/D1+](https://jethome.ru/d1p) (Basic version with 3 relays, 4 inputs and 1-wire, 1 ZigBee module).

**Exposed peripheral:**

- 3 relays
- 4 inputs
- internal stat LED (green/red)
- (optional) ZigBee module control (BOOT, RESET)

### [JetHome JetHub H1](https://jethome.ru/h1) (Basic version, ZigBee module)

**Exposed peripheral:**

- internal stat LED
- (optional) modules slot control (BOOT, RESET)

### [JetHome JetHub D3](https://docs.iot.jethome.com) (modular controller, 4 UXM slots)

**Exposed peripheral:**

- UXM slots control (RESET, MODE)


## JetHome resources:

- Documentation - https://docs.jethome.com
- Official website - https://jethome.com
- Telegram news channel - https://t.me/jethome_news
- Telegram english news channel - https://t.me/jethome_iot_news
- Telegram official chat - https://t.me/jethomeru
- Telegram official english chat - https://t.me/jethome_iot
- GitHub: https://github.com/jethome-iot

[maintenance-shield]: https://img.shields.io/maintenance/yes/2026.svg
[project-stage-shield]: https://img.shields.io/badge/project%20stage-production%20ready-brightgreen.svg
[release-shield]: https://img.shields.io/badge/version-v1.0.1-blue.svg
[release]: https://github.com/jethome-hassio-addons/addon-jethub-gpio2mqtt/tree/v1.0.1