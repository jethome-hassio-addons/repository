# JetHome Home Assistant Add-ons

![Project Stage][project-stage-shield]
![Maintenance][maintenance-shield]

## Installation

Adding this add-ons repository to your Home Assistant instance is
pretty straightforward. In the Home Assistant add-on store,
a possibility to add a repository is provided.

Use the following URL to add this repository:

```txt
https://github.com/jethome-hassio-addons/repository
```

## Add-ons provided by this repository

### &#10003; [JetHome JetHub mqtt-io peripheral exposer][addon-jethub-mqtt-io]

![Latest Version][jethub-mqtt-io-version-shield]
![Supports aarch64 Architecture][jethub-mqtt-io-aarch64-shield]
![Supports amd64 Architecture][jethub-mqtt-io-amd64-shield]

DEPRECATED - replaced by JetHome peripheral exposer. Expose JetHome JetHub peripheral via mqtt-io

[:books: JetHome JetHub mqtt-io peripheral exposer add-on documentation][addon-doc-jethub-mqtt-io]

### &#10003; [JetHome peripheral exposer][addon-jethub-gpio2mqtt]

![Latest Version][jethub-gpio2mqtt-version-shield]
![Supports aarch64 Architecture][jethub-gpio2mqtt-aarch64-shield]
![Supports amd64 Architecture][jethub-gpio2mqtt-amd64-shield]

Expose JetHome JetHub (D1/D2/D3/H1) peripheral (relays, inputs, UXM control) via gpio2mqtt

[:books: JetHome peripheral exposer add-on documentation][addon-doc-jethub-gpio2mqtt]

## Releases

Releases are based on [Semantic Versioning][semver], and use the format
of ``MAJOR.MINOR.PATCH``. In a nutshell, the version will be incremented
based on the following:

- ``MAJOR``: Incompatible or major changes.
- ``MINOR``: Backwards-compatible new features and enhancements.
- ``PATCH``: Backwards-compatible bugfixes and package updates.

## Support

- [Open an issue for the add-on: JetHome JetHub mqtt-io peripheral exposer][jethub-mqtt-io-issue]
- [Open an issue for the add-on: JetHome peripheral exposer][jethub-gpio2mqtt-issue]

[addon-jethub-mqtt-io]: https://github.com/jethome-hassio-addons/addon-jethub-mqtt-io/tree/v0.3.1
[addon-doc-jethub-mqtt-io]: https://github.com/jethome-hassio-addons/addon-jethub-mqtt-io/blob/v0.3.1/README.md
[jethub-mqtt-io-issue]: https://github.com/jethome-hassio-addons/addon-jethub-mqtt-io/issues
[jethub-mqtt-io-version-shield]: https://img.shields.io/badge/version-v0.3.1-blue.svg
[jethub-mqtt-io-aarch64-shield]: https://img.shields.io/badge/aarch64-yes-green.svg
[jethub-mqtt-io-amd64-shield]: https://img.shields.io/badge/amd64-no-red.svg
[addon-jethub-gpio2mqtt]: https://github.com/jethome-hassio-addons/addon-jethub-gpio2mqtt/tree/v1.0.0
[addon-doc-jethub-gpio2mqtt]: https://github.com/jethome-hassio-addons/addon-jethub-gpio2mqtt/blob/v1.0.0/README.md
[jethub-gpio2mqtt-issue]: https://github.com/jethome-hassio-addons/addon-jethub-gpio2mqtt/issues
[jethub-gpio2mqtt-version-shield]: https://img.shields.io/badge/version-v1.0.0-blue.svg
[jethub-gpio2mqtt-aarch64-shield]: https://img.shields.io/badge/aarch64-yes-green.svg
[jethub-gpio2mqtt-amd64-shield]: https://img.shields.io/badge/amd64-yes-green.svg

[issue]: https://github.com/jethome-hassio-addons/repository/issues
[license-shield]: https://img.shields.io/github/license/jethome-hassio-addons/repository.svg
[maintenance-shield]: https://img.shields.io/maintenance/yes/2026.svg
[project-stage-shield]: https://img.shields.io/badge/project%20stage-production%20ready-brightgreen.svg
[semver]: http://semver.org/spec/v2.0.0.html