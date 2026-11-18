Faster turbine calibration approach.

- Calibration now climbs toward both 900 and 1800 RPM with coils OFF, then engages them shortly before reaching the target.
- Final settling and the 30-second stable-flow verification still use engaged coils, so saved flows describe actual power generation.
- The measured 900 RPM flow seeds the 1800 RPM test instead of relying only on the initial short probe.
- Cancel, original power/settings restoration, interrupted-test recovery, shortage detection and overspeed handling remain in place.

Validated with 59 calibration checks plus per-sample acceleration assertions, 38 baseline RPM checks, fleet monitor interaction and Load Match regression checks. A slow-rotor simulation verifies unloaded acceleration at both target speeds and loaded steady measurements. Actual calibration duration depends on the turbine and steam supply; live hardware testing is ongoing.

Cancel the current test, install through INFO > UPDATES, reboot from the CC terminal, then restart calibration with steam supplied and condensate draining. Existing profiles are retained; run START TEST if you want fresh measurements.
