# Home Assistant Add-on: JetHome JetHub peripheral exposer

[![Release][release-shield]][release] ![Project Stage][project-stage-shield] ![Project Maintenance][maintenance-shield]

## About

Expose [JetHub](http://jethome.ru) resources (relays,inputs,etc..) to Home Assistant via [mqtt-io](https://github.com/flyte/mqtt-io)

**Note**: _All used GPIOs will **disappear** from **/sys/class/gpio** during addon run_

## Supported devices:

### [JetHome JetHub D1](http://jethome.ru/jethub-d1) (Basic version with 3 relays, 4 inputs and 1-wire).

**Exposed peripheral:**

- 3 relays
- 4 inputs
- internal stat LED (green/red)

**Note**: _You still need to use native Home Assistant [1-Wire](https://www.home-assistant.io/integrations/onewire/) integration to expose 1-Wire device 
like temperature sensors `DS18B20`_


## JetHome resources:

- Documentation - https://wiki.jethome.ru
- Official website - http://jethome.ru
- Telegram news channel - https://t.me/jethome_news
- Telegram official chat - https://t.me/jethomeru
- GitHub: https://github.com/jethome-ru

[maintenance-shield]: https://img.shields.io/maintenance/yes/2023.svg
[project-stage-shield]: https://img.shields.io/badge/project%20stage-production%20ready-brightgreen.svg
[release-shield]: https://img.shields.io/badge/version-v0.2.4-blue.svg
[release]: https://github.com/jethome-hassio-addons/addon-jethub-mqtt-io/tree/v0.2.4