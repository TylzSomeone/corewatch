Simpler turbine calibration and RPM selection.

- START TEST turns the selected turbine on when needed, after checking steam, condensate and profile storage.
- Choosing 900 or 1800 RPM with no valid profile starts calibration automatically, then runs at the chosen speed after a successful test. Outdated profiles also trigger a new test. Known unreachable targets remain clearly rejected.
- Choosing a calibrated speed turns the turbine on if needed.
- Standalone calibration restores previous settings when finished. Cancel and failure restore previous settings, including returning to OFF if the test started the turbine. Overspeed parks steam at zero with coils engaged.
- Restart/reconnect restores interrupted settings without restarting calibration or continuing a pending RPM selection. Reactors remain independent.

Validated with 55 turbine calibration checks, 38 baseline RPM checks, fleet monitor interaction and Load Match regression checks. Live hardware testing is ongoing.

Install through INFO > UPDATES, then reboot from the CC computer terminal. Keep steam supplied and condensate draining, then choose 900/1800 RPM or CALIBRATE / PROFILE > START TEST.
