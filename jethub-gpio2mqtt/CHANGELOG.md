## Fix

- **AppArmor profile fixed: scripts use `rix` instead of `ix`.** The `ix` permission grants the execute transition but not the read permission, and a shebang script is read by its interpreter — so 1.0.1 failed to start with `/bin/bash: /usr/local/bin/entrypoint.sh: Permission denied`.

Verified on hardware and locally (profile loaded in the kernel, add-on image runs confined with the entrypoint executing normally).

If you are on 1.0.1: update to this version. If you stayed on 1.0.0: update as usual — 1.0.2 includes the AppArmor hardening from 1.0.1 in working form (security rating 8/8).