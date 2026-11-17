Opt-in automatic turbine RPM control.

- Choose MANUAL, 900 RPM or 1800 RPM independently for each turbine.
- RPM mode adjusts steam intake gradually and considers rotor acceleration when approaching the target.
- Selecting a target never starts the turbine or changes coil engagement. It waits while the turbine or coils are off.
- Reports steam-supply limits, full condensate storage and maximum flow.
- Manual flow changes, OFF or COILS OFF disarm RPM mode. MANUAL keeps the current flow setting. Startup and reconnect return to Manual without changing hardware settings.
- The steam reactor stays under independent manual control; this release does not coordinate reactor steam production.

Validated with delayed rotor simulations for both targets, varying response times and load, bounded flow changes, starvation, capacity limits, manual overrides, link failures and safe startup. Multi-machine monitor routing and the RF Load Match regression checks also pass. Live tuning may vary with turbine construction; try 900 RPM first and observe its response.

Install through INFO > UPDATES > CHECK > INSTALL, then open the CC computer terminal and hold Ctrl+R there. Existing reactor and monitor settings are preserved.
