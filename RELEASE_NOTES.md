Automatic steam supply for paired turbines.

- Steam-reactor page: PAIR opens a paginated list of discovered turbines. Tap turbines to pair/unpair, then BACK. Pairings are saved per reactor, and a turbine cannot be assigned to two reactors.
- Tap AUTO OFF to enable AUTO ON. Automatic supply adjusts all reactor rods toward combined configured flow of active paired turbines, plus a modest steam reserve. Configured demand still counts when a turbine is steam-starved or accelerating.
- NEED / PRODUCED and supply status appear on the existing 4x3 reactor dashboard. The dedicated turbine monitor remains independent.
- Idle turbines stop generation after reserve is ready; a low idle reserve can refill for startup. Full steam, missing fuel and low coolant pause generation with restart thresholds. Zero rods with unmet demand reports reactor capacity.
- Manual power/rod controls leave automatic supply. Changing pairing requires Manual. An external reactor OFF also disarms supply.
- Missing or unreadable paired turbines stop their reactor, fully insert rods and disarm Auto Supply. Lost reactor links also disarm it. Reboot starts steam control in Manual with saved pairings retained; enable Auto again when ready.
- Existing RF modes, turbine calibration profiles and RPM control remain available. Still one downloadable corewatch file; no manual peripheral names or file edits required.

Setup: update and reboot, open the steam reactor under MACHINES, PAIR its physically connected turbines, BACK, then tap AUTO OFF to enable. Keep coolant supplied and steam/condensate piping connected. Let the initial steam reserve build before starting turbine calibration or selecting an RPM.

Validated with 36 steam-supply checks, touchscreen pairing/persistence/duplicate-claim and lost-link integration tests, thermal-response simulations, 77 turbine calibration/startup checks, 38 baseline RPM checks and existing fleet/Load Match regressions. Both reactor and pairing layouts were visually checked at 79x38. Live hardware tuning is ongoing.
