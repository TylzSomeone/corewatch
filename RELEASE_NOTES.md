Per-turbine calibration and automatic coil handling.

- CALIBRATE / PROFILE > START TEST measures coast, acceleration, coil braking and stable flow at 900 and 1800 RPM.
- Saved profiles are specific to each turbine. Calibrated RPM mode unloads coils during initial acceleration, engages them before the target, and keeps them engaged while braking with reduced steam.
- Measured steady flows provide the starting point; fine correction handles small differences. Without calibration, existing gentle flow-only RPM control remains available.
- Detected rotor/hardware changes invalidate profiles. Coil-only changes require recalibration; persistent changed response can flag a profile check.
- Test progress and cancellation are available on the monitor. Cancel and completion restore previous flow and coils. A working lower target survives an unreachable upper target.
- Interrupted calibration or unloaded spin-up has a durable restoration marker, so settings are restored after reboot or reconnect. Turbine power is never switched on automatically. Normal startup remains Manual.
- Blocked condensate, inadequate steam, timeout and overspeed have explicit outcomes. Overspeed stops calibration at zero flow with coils engaged.

To calibrate: turbine ON, steam supplied continuously, condensate able to leave, then CALIBRATE / PROFILE > START TEST. The test changes flow/coils and can take several minutes. The steam reactor remains independent.

Validated with 40 calibration checks and 38 baseline RPM checks, physical rotor simulations at several response speeds, main/dedicated monitor interactions, per-turbine persistence and interrupted-test recovery. Fleet and Load Match regression checks also pass. Live hardware testing is ongoing.

Install through INFO > UPDATES > CHECK > INSTALL, then open the CC computer terminal and hold Ctrl+R there. One downloadable corewatch file still contains the full program; profiles are kept in the existing machine registry.
