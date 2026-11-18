A clearer system overview and easier navigation.

- The main screen now shows total power, separate direct-reactor/turbine contributions, and fleet steam needed versus produced. RF and FE contributions are displayed as RF/t.
- ALL / REACTORS / TURBINES / ATTENTION filters keep the list focused. Rows use plain status labels such as Stable, Building reserve, Accelerating, Steam shortage, Manual and Off.
- Steam reactors list the turbines they supply. Turbine rows name their paired steam reactor, and show current RPM versus the selected target.
- Tap anywhere on a machine row to open its controls. The top-left OVERVIEW button returns to the same filter/page. MONITORS is available at the bottom right; large fleets use PREV / NEXT.
- Offline and stale readings are excluded from totals and clearly identified. Overview drawing uses worker snapshots without peripheral queries or control commands.
- Existing machine controls, saved settings, steam pairings and turbine calibration profiles are retained. First-run reactor migration remains available.

Validated with 29 overview checks, live touchscreen filter/navigation/routing checks, 40-reactor pagination and 4x3 layout previews. Existing fleet/update/migration, 42 steam-supply, 77 turbine calibration/startup, 38 baseline RPM and Load Match checks pass.

Install through INFO > UPDATES on an RF reactor page, then reboot from the CC terminal. Steam Auto and turbine RPM modes still require re-enabling after reboot; saved pairings and calibration remain usable.
