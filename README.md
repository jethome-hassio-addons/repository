# JetHome Home Assistant Add-ons

![Project Stage][project-stage-shield]
![Maintenance][maintenance-shield]

<https://github.com/jethome-ru/hassio-repository>

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
![Supports armhf Architecture][jethub-mqtt-io-armhf-shield]
![Supports armv7 Architecture][jethub-mqtt-io-armv7-shield]
![Supports aarch64 Architecture][jethub-mqtt-io-aarch64-shield]
![Supports amd64 Architecture][jethub-mqtt-io-amd64-shield]
![Supports i386 Architecture][jethub-mqtt-io-i386-shield]

Expose JetHome JetHub peripheral (relays, inputs, etc..) via mqtt-io

[:books: JetHome JetHub mqtt-io peripheral exposer add-on documentation][addon-doc-jethub-mqtt-io]

## Releases

Releases are based on [Semantic Versioning][semver], and use the format
of ``MAJOR.MINOR.PATCH``. In a nutshell, the version will be incremented
based on the following:

- ``MAJOR``: Incompatible or major changes.
- ``MINOR``: Backwards-compatible new features and enhancements.
- ``PATCH``: Backwards-compatible bugfixes and package updates.

The beta add-ons will also have an additional beta marker, unless, the
stable release is newer, in that case, the stable release is published
in this channel.

## Support

- [Open an issue for the add-on: JetHome JetHub mqtt-io peripheral exposer][jethub-mqtt-io-issue]

[addon-jethub-mqtt-io]: https://github.com/jethome-hassio-addons/addon-jethub-mqtt-io/tree/v0.2.4
[addon-doc-jethub-mqtt-io]: https://github.com/jethome-hassio-addons/addon-jethub-mqtt-io/blob/v0.2.4/README.md
[jethub-mqtt-io-issue]: https://github.com/jethome-hassio-addons/addon-jethub-mqtt-io/issues
[jethub-mqtt-io-version-shield]: https://img.shields.io/badge/version-v0.2.4-blue.svg
[jethub-mqtt-io-aarch64-shield]: https://img.shields.io/badge/aarch64-yes-green.svg
[jethub-mqtt-io-amd64-shield]: https://img.shields.io/badge/amd64-no-red.svg
[jethub-mqtt-io-armhf-shield]: https://img.shields.io/badge/armhf-no-red.svg
[jethub-mqtt-io-armv7-shield]: https://img.shields.io/badge/armv7-no-red.svg
[jethub-mqtt-io-i386-shield]: https://img.shields.io/badge/i386-no-red.svg

[issue]: https://github.com/jethome-hassio-addons/repository/issues
[license-shield]: https://img.shields.io/github/license/jethome-hassio-addons/repository.svg
[maintenance-shield]: https://img.shields.io/maintenance/yes/2023.svg
[project-stage-shield]: https://img.shields.io/badge/project%20stage-production%20ready-brightgreen.svg
[semver]: http://semver.org/spec/v2.0.0.html