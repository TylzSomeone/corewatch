Automatic turbine discovery and a dedicated turbine monitor.

- Detects connected Extreme Reactors turbine ports at startup and when attached later.
- One spare monitor is assigned to turbines automatically. MACHINES > MONITORS selects or disables the dedicated display without editing files.
- Shows RPM, output and history, stored energy, steam, condensate, flow, blade count and efficiency.
- Manual ON/OFF, coil engagement, flow steps and typed flow limits. Input is checked against the port's hardware maximum, and every write rechecks the exact target.
- Turbine state and settings are preserved at startup and reconnect. Reactors keep their independent controllers; a missing turbine or second monitor does not stop them.
- Multiple turbines can be selected on either the main console or the dedicated screen.

This release adds manual turbine control. Automatic RPM control, steam regulation and reactor/turbine pairing are future work.

Validated with the installed Extreme Reactors 2.4.28 peripheral API, simulated fleets of 40 reactors and two turbines, isolated touch routing, flow validation, disconnect/reconnect, monitor resize, saved assignments and safe reboot. The Load Match regression simulation also passes. Live turbine testing is ongoing.

Install through INFO > UPDATES > CHECK > INSTALL, then open the CC computer terminal and hold Ctrl+R there. Existing reactor settings are preserved. The turbine and spare monitor are detected automatically after reboot.
