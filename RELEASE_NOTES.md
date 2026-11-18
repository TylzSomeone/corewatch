Quicker loaded settling during turbine calibration.

- Coil engagement during the approach is limited to the final 1.5% of the test speed, rather than potentially switching around 800 RPM for the 900 RPM test.
- Once engaged, calibration uses measured acceleration to adjust loaded steam flow. It no longer uses the normal operating loop's cautious 90-second lookahead for this test stage.
- Loaded flow changes remain bounded to 5% of the hardware flow limit per sample. The final stable-flow verification still lasts 30 seconds with coils engaged.
- Normal calibrated RPM operation, cancel/restoration, shortage detection, overspeed handling and restart recovery remain in place.

Validated with 65 calibration checks plus per-sample assertions, 38 baseline RPM checks, fleet monitor interaction and Load Match regression checks. The slow-rotor simulation that previously spent 196 seconds between engagement and 900 RPM verification now begins verification two seconds after engagement; actual hardware timing will vary. Both targets and imperfect acceleration estimates are covered.

Cancel the current test, install through INFO > UPDATES, reboot from the CC terminal, then restart calibration with steam supplied and condensate draining.
