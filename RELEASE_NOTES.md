Smoother low-load steam matching.

- Normal steam matching uses individual 1% rod steps with at least six seconds of settling between moves, rather than jumping back and forth by 3%.
- Smoothed production readings prevent small per-sample fluctuations from becoming large alternating trend corrections.
- Larger adjustments, up to 3%, remain available for substantial oversupply or a serious shortage. Full-reserve parking and manual controls can still move rods directly.
- Restart after a full steam tank uses a more conservative rod setting based on demand and learned reactor response, instead of immediately resuming the excessive output.
- Fractional corrections at 0/100% rod insertion can accumulate inward again, avoiding a controller stuck at the boundary.
- Pairing, calibration profiles, manual overrides, coolant/fuel pauses and lost-link handling are retained.

Validated with 42 steam-supply checks, including a noisy 500-550 mB/t reactor supplying a 380 mB/t turbine. The model settles with individual rod steps and no repeated late power cycling. Also passed thermal-response simulations, touchscreen/fleet tests, 77 turbine calibration/startup checks, 38 baseline RPM checks and Load Match regressions. Live hardware response may differ.

Install through INFO > UPDATES, reboot, then re-enable Auto on the steam-reactor page. Saved pairings and turbine calibration remain usable.
