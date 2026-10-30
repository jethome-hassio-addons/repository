## Fixes for Armbian / HA Supervised installs (issue #2)

On systems where GPIO lines are held via the sysfs interface (e.g. left by the legacy sysfs-based add-on on official JetHome Armbian images), gpiod requests fail with `Device or resource busy`. Two problems were fixed:

- **GPIO-unexport helper: sysfs chip base resolution** now handles the modern kernel 6.x topology (checks the resolved device directory first), keeps the legacy layouts as fallbacks, and adds a chip-label fallback (label read via the GPIO uAPI ioctl). If the base cannot be resolved while the sysfs GPIO interface is active, it fails loudly with a manual-unexport hint instead of silently doing nothing.
- **AppArmor profile** now allows reading the sysfs GPIO chip directories under `/sys/devices` that the device symlinks resolve to.

Verified on hardware: JetHub D1+ (Armbian 24.11 bookworm, kernel 6.6, HA Supervised).