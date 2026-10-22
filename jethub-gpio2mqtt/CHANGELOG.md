## Security

- **AppArmor enabled with a dedicated profile** (`apparmor.txt`): the add-on now runs confined instead of unconfined. The profile allows exactly the add-on access surface — gpiod character devices, legacy sysfs GPIO unexport, device tree reads for model detection, I²C topology for the JetHub D3 expander auto-resolve, and MQTT/Supervisor networking.
- Supervisor security rating **6 → 8** (maximum), the red AppArmor badge is gone.

No functional changes. Daemon: gpio2mqtt 0.2.2.