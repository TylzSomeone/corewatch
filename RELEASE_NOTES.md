Close-to-target coil engagement during normal RPM startup.

- Saved-profile 900/1800 RPM startup now uses the same coil-engagement threshold as calibration: within the final 1.5% of the target.
- Removes the old long engagement lead from normal spin-up, including when an existing saved profile contains that value.
- Already-spinning rotors below 98.5% of the chosen target also use unloaded acceleration rather than immediately engaging coils.
- Existing calibration profiles remain valid. No recalibration is needed for this update.
- Braking, loaded fine control, manual overrides and interrupted-spin-up restoration remain unchanged.

Validated with 77 calibration/normal-startup checks, 38 baseline RPM checks, fleet monitor interaction and Load Match regression checks. New tests cover both targets from stopped and already-spinning rotors with old long-lead profile data. Hardware timing and overshoot depend on rotor response and sampling.

Install through INFO > UPDATES, reboot from the CC terminal, then select 900 or 1800 RPM with your existing profile.
