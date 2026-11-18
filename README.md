# Corewatch

Corewatch is a touchscreen dashboard and controller for Extreme Reactors in Minecraft. See what your reactor is producing, what your base is drawing, and how much fuel you have left, all from one monitor wall. Manage multiple reactors and turbines independently, with a dedicated turbine monitor when a spare screen is connected.

![Corewatch dashboard showing power history, buffer, control rods, fuel, and waste](dashboard.png)

## What it does

- Graphs generation in RF/t and shows stored energy, net buffer change, and estimated RF out.
- Tracks fuel, estimated runtime, fuel efficiency, and waste.
- Compares energy, fuel burn, efficiency, and duty cycle across modes in **INFO → STATS**.
- Saves your buffer limits, RF/t target, boot mode, and sound preference.
- Reconnects when each reactor port returns without stopping other controllers, and can check GitHub for updates.
- Lists connected reactors under **MACHINES**, with separate settings, names, histories, and RF session statistics.
- Detects steam reactors, shows steam/coolant readings, and provides manual controls or automatic supply for paired turbines.
- Automatically discovers turbines and shows RPM, output, stored energy, steam/water, blade efficiency and flow.
- Provides manual turbine controls, per-turbine calibration and opt-in 900/1800 RPM regulation with automatic coil handling.
- Assigns one spare monitor to turbines automatically; choose or disable it under **MACHINES → MONITORS**.

## Control modes

| Mode | What it does |
| --- | --- |
| **Auto** | Adjusts the rods as the internal buffer fills. MIN is where throttling begins, and MAX is where the rods reach full insertion. |
| **Manual** | Holds rod position until you adjust it. Use the ±10% or ±1% buttons. |
| **Target RF/t** | Tracks an output you choose and backs off at MAX. Tap the RF/t setpoint to enter a number. |
| **Standby** | When armed, starts the reactor at or below MIN and shuts it off at MAX. DISARM shuts it down and disables automatic starts. |
| **Load Match** | Follows estimated demand to keep NET near zero. Below MIN it aims for a surplus, and MAX caps buffer fill. |

![Corewatch mode menu with Auto, Manual, Target RF/t, Standby, and Load Match](mode-menu.png)

Tap **MODE → BOOT MODE** to choose what opens after a reboot. New reactors default to Manual. Each reactor has its own saved boot mode. Standby boots disarmed. Tap **ARM** when you want it to manage starts. Tap the MIN and MAX values to enter them directly where those controls are available.

## Setup

- **Reactors:** One or more Extreme Reactors reactors with **Reinforced Reactor Computer Ports**. Direct RF reactors retain all five control modes. Steam reactors support manual controls and opt-in automatic supply for paired turbines.
- **Turbines:** Reinforced Turbine Computer Ports shared through enabled wired modems. Turbines are discovered automatically; no peripheral names to enter or files to edit.
- **Computer:** A CC: Tweaked computer connected directly to the reactor port or through a wired modem network. Enable peripheral access on the wired modem attached to the port.
- **Display:** **4 blocks wide by 3 blocks tall** is recommended for the main console. A dedicated turbine screen supports **2×2 or larger** at scale 0.5. The spare monitor is optional; turbine pages also open on the main console.
- **Sound:** Optional CC: Tweaked Speaker, connected directly or over the wired network. Toggle cues under **MODE**.

This setup was used on **All the Mods 10 v8.4**.

## Install

Run these commands in the CC computer's terminal. The server must allow CC: Tweaked HTTP downloads from GitHub.

```text
wget https://github.com/TylzSomeone/corewatch/releases/latest/download/corewatch corewatch
corewatch
```

Corewatch keeps the original reactor's configuration in `corewatch-settings.txt`, stores other reactor configurations separately, and records names and assignments in `corewatch-machines.txt`. Back up these files together. To launch automatically, add this line to your CC computer's `startup` file.

```lua
shell.run("corewatch")
```

## Multiple reactors

Tap **MACHINES** in the persistent top bar to select a reactor. All controllers continue working while you browse another dashboard or the paginated machine list. Tap **ALERTS** in the top bar or machine overview to see affected reactor names, ports, specific problems, and suggested checks. Use **OPEN REACTOR** to jump to that machine; **BACK** returns to the previous view. The list updates as faults clear and supports multiple pages. The count represents affected reactors. Current conditions include paused automatic steam supply, fuel below 5% (with a distinct empty-fuel message), lost links, incomplete assemblies, paused controllers, and unreadable ports. New ports are discovered automatically; saved missing ports remain listed for diagnosis.

When upgrading an existing installation with several reactors connected, first select the **original reactor** to inherit your old settings. Controllers wait for that choice. Other RF reactors begin in **Manual** and retain their existing power state and rod positions until you change them. Configure each reactor's boot mode separately.

Use **RENAME** on a reactor page, type a name at the CC computer, and press Enter. Escape cancels. Assignments are tied to exact peripheral names; check them after replacing or moving computer ports.

Steam reactors show a thin teal production-history trace in mB/t, percentage gauges for steam and coolant, a rod insertion bar, fuel, waste, temperatures, and full touch buttons for power and ±10%/±1% rod adjustments. The graph adds a sample every two seconds; button presses do not add samples. Empty tanks are labeled EMPTY. Pair turbines and enable Auto Supply to regulate steam production for their combined flow demand. The main console can show any machine, and a spare monitor can separately show turbines.

## Automatic steam supply

Open your steam reactor under **MACHINES**, tap **PAIR**, and tap each turbine physically supplied by that reactor. A reactor may feed several turbines; a turbine can be paired with only one reactor. Pairing choices are saved in `corewatch-machines.txt`. The list supports multiple pages. Pairing tells Corewatch which demand belongs to the reactor; it does not create fluid connections or route steam. Connect steam pipes and a coolant/condensate return yourself.

Tap **BACK**, then **AUTO OFF** to switch it to **AUTO ON**. This explicitly allows the reactor to start, stop and adjust all its rods together. The dashboard shows combined **NEED** and **PRODUCED** in mB/t, plus its current supply status. Existing turbine profiles and speed controls are unchanged.

Auto Supply uses each active paired turbine's configured flow, including during unloaded acceleration or calibration, so a steam-starved turbine still contributes its requested demand. A stopped turbine or one with a full water outlet contributes no demand. Production is adjusted toward demand plus a modest reserve around 30% of the reactor's internal steam tank. Rod changes are bounded to three percentage points per two-second sample, using production trend to avoid chasing thermal lag.

When turbines are idle, the reactor stops with rods fully inserted once reserve is ready; it refills from below 15% toward 30% so there is steam for the next startup. Allow the initial reserve to build before starting turbine calibration. A steam tank at 90% pauses generation until it falls to 65%. Missing fuel or nearly empty coolant also pauses generation; coolant must recover above 10% before restarting. These pauses resume automatically while Auto Supply remains enabled. If production cannot meet demand at zero rod insertion, the screen reports the reactor steam limit. Full reactor steam with starving turbines can indicate a pipe throughput or connection problem.

Tap **AUTO ON** to return to Manual. The reactor's ON/OFF or rod buttons also leave Auto Supply before applying your manual command. Switch to Manual before editing pairs. An external reactor OFF disables automatic supply rather than restarting it.

A missing or unreadable paired turbine makes its reactor stop, fully insert rods and disable Auto Supply. Reconnect it and select Auto again. A lost reactor link also disarms its automatic supply. Other reactors keep their independent controls. **Reboot always starts steam reactors in Manual**, preserving physical power/rod settings and saved pairings; enable Auto again when ready. This does not change the existing RF boot modes.

## Turbines and monitor discovery

Connect each turbine computer port to the same enabled wired network. **MACHINES** discovers new turbine ports automatically, including ports attached while Corewatch runs. Missing registered ports remain listed for diagnosis. Turbine readings update every two seconds.

With one spare monitor, Corewatch assigns it to turbines automatically and saves that role. A missing assigned screen is waited for; another screen is not silently substituted. With several spare monitors, choose one under **MACHINES → MONITORS**. The same menu can disable the dedicated screen. Monitor roles and the selected turbine persist in `corewatch-machines.txt`.

Tap **TURBINES** on the dedicated screen to switch turbines. Its dashboard shows RPM, FE/t output and history, stored energy, steam and condensate, actual flow, configured flow limit, blade count and efficiency.

Use separate ON/OFF and COILS ON/OFF controls. OFF does not instantly brake the rotor. Flow steps adjust by 10 or 100 mB/t. Tap FLOW, type a whole number at the CC computer, and press Enter; Escape cancels. The port's hardware maximum is enforced and the exact target is checked again before each write.

Turbines retain their active state, coil state and flow settings at startup and reconnect. Each turbine starts in **Manual**. Select **900 RPM** or **1800 RPM** to regulate speed by gradually adjusting steam intake. Selecting a target turns the turbine on when needed and starts calibration if there is no valid saved profile.

Choosing 900 or 1800 RPM without a valid saved profile starts calibration, then continues at the selected speed after a successful test. With calibration, it uses measured flow, acceleration and braking response, disengages coils during initial acceleration, and re-engages them within the final 1.5% of the target, using the same engagement rule as calibration. Deceleration keeps coils engaged and cuts steam, then returns to the measured flow near the target. Fine flow corrections are limited to about 1% of the hardware maximum, capped at 25 mB/t per sample. Calibrated startup can select a measured flow directly and use a temporary steam boost; braking can cut flow to zero. It reports insufficient steam, full condensate storage or the hardware flow limit instead of continually increasing demand. Manual flow changes, OFF and COILS OFF cancel RPM mode. MANUAL retains the current flow setting. A failed turbine link disarms RPM mode; opt in again after reconnecting.

### Calibrating a turbine

Supply steam continuously and make sure condensate can leave. Open **CALIBRATE / PROFILE** and select **START TEST**. Calibration changes flow and coil engagement; unloading coils temporarily stops power generation. START TEST turns the turbine on if needed. The test controls the turbine; a paired reactor in Auto Supply independently follows its changing steam demand.

The staged test measures unloaded coast, acceleration and coil braking, then climbs toward each test speed with coils disengaged. Coils engage within the final 1.5% of the target. Calibration uses measured acceleration to correct loaded flow while settling, then verifies stable loaded flow at 900 and 1800 RPM. The measured 900 RPM flow helps estimate the 1800 RPM starting flow. Progress and elapsed time appear on the profile page; BACK lets you watch the normal dashboard while the test continues. **CANCEL TEST** restores the previous flow, coils and original OFF state if the test started the turbine. Failure restores those settings too, except overspeed parks steam at zero with coils engaged. A standalone START TEST restores settings and returns to Manual when complete; a test started by choosing an RPM continues at that speed after successful calibration. Slow rotors can take several minutes to settle.

Each turbine's measured profile is saved separately in `corewatch-machines.txt`. A valid 900 RPM result is retained if 1800 RPM exceeds available capacity. Insufficient steam, blocked condensate, changing hardware or failure to settle are reported rather than saved as working targets. An overspeed abort parks flow at zero with coils engaged. Other interrupted tests retain a saved restoration marker; startup or reconnect restores those settings without turning turbine power on.

Choosing a calibrated RPM also turns the turbine on if needed. Startup and reconnect still default to Manual; they do not restart calibration or remember a pending speed selection. An interrupted test restores flow/coils and turns the turbine back off if it was originally OFF. If interrupted during unloaded automatic spin-up, the saved loaded flow and engaged coils are restored before returning to Manual.

Blade count, rotor mass, maximum flow and known variant/fluid readings identify the calibrated setup. Detectable changes invalidate the profile and require recalibration. Coil material/count are not exposed by the installed port, so **recalibrate after changing coils**. Persistent flow drift can recommend a profile check, but does not prove which block changed.

Automatic steam supply is available through the steam-reactor page; vent-setting controls are future work. RF modes still control only direct-power reactors. The RPM loop, API behavior and monitor routing are covered by simulations; real hardware testing is ongoing. Start with 900 RPM when trying it on a new setup and observe the response.

There is no fixed reactor-count limit in the code. Automated simulations covered 40 reactors and two independently controlled turbines, but real-world capacity depends on the computer, modpack, and wired network. Each controller has a staggered refresh cycle and physical monitor writes are limited to changed rows.

## Updates

Open **INFO → UPDATES → CHECK**. Turn on **BOOT CHECK** if you want Corewatch to check each time it starts. When it finds a newer release, the dashboard's **INFO** button becomes **UPDATE** and opens the update screen.

Tap **INSTALL** when you're ready. Then **open the CC computer's terminal and hold Ctrl+R there**. The new version starts after reboot and keeps your saved settings.

## Troubleshooting

- **Reactor missing:** Run `peripherals` in the CC terminal. Check the cable and enable peripheral access on the modem attached to the Reinforced Reactor Computer Port.
- **Monitor missing:** Connect the Advanced Monitor wall directly or enable its wired modem. Use the 4×3 layout if text or controls look cramped.
- **Download or update fails:** Check whether CC: Tweaked HTTP is enabled and whether the server permits GitHub downloads. You can also download the `corewatch` file from Releases and copy it to the CC computer.
- **Standby waits after a reboot or a lost link:** Tap **ARM** to allow automatic starts again.

## Update log

- **[v1.21.0](https://github.com/TylzSomeone/corewatch/releases/tag/v1.21.0)** — Saved touchscreen reactor-to-turbine pairing and opt-in automatic steam supply. Matches combined configured flow, maintains a small reserve, pauses for idle turbines/full steam/missing coolant or fuel, and disarms on lost pairs. Shows needed versus produced steam on the 4×3 reactor page.

- **[v1.20.4](https://github.com/TylzSomeone/corewatch/releases/tag/v1.20.4)** — Normal saved-profile startup now shares calibration’s close-to-target coil engagement. Already-spinning rotors also accelerate unloaded when below the final approach band. Existing profiles remain usable without recalibration.

- **[v1.20.3](https://github.com/TylzSomeone/corewatch/releases/tag/v1.20.3)** — Calibration engages coils closer to each target and uses measured acceleration for loaded settling, avoiding the long slow tail after early coil engagement. Normal calibrated RPM control is unchanged.

- **[v1.20.2](https://github.com/TylzSomeone/corewatch/releases/tag/v1.20.2)** — Calibration now accelerates with coils OFF toward both test speeds, then engages coils near the target to measure generating flow. Uses the measured 900 RPM flow to seed the 1800 RPM test.

- **[v1.20.1](https://github.com/TylzSomeone/corewatch/releases/tag/v1.20.1)** — START TEST powers on the selected turbine when needed. Choosing an uncalibrated RPM starts calibration and continues at that speed on success. Cancel, failure and restart restore the earlier settings without resuming a pending speed selection.

- **[v1.20.0](https://github.com/TylzSomeone/corewatch/releases/tag/v1.20.0)** — Per-turbine calibration measures acceleration, braking and stable 900/1800 RPM flows. Saved profiles drive faster startup with automatic coils, loaded braking and fine correction. Adds profile invalidation, cancel/progress controls and durable recovery after interrupted tests.

- **[v1.19.0](https://github.com/TylzSomeone/corewatch/releases/tag/v1.19.0)** — Opt-in 900/1800 RPM regulation for each turbine, gradual steam-flow adjustments, acceleration-aware control and clear steam/flow-limit status. Manual overrides and disconnects disarm RPM mode; boot remains Manual.

- **[v1.18.0](https://github.com/TylzSomeone/corewatch/releases/tag/v1.18.0)** — Automatic turbine discovery, manual turbine controls and a dedicated turbine monitor. One spare display is assigned automatically; monitor roles and turbine selection are saved. Flow input validates against the hardware maximum. Startup and reconnect preserve turbine settings. Automatic RPM/steam regulation remains future work.

- **[v1.17.4](https://github.com/TylzSomeone/corewatch/releases/tag/v1.17.4)** — Fixed Load Match repeatedly closing the rods while the buffer is empty or below MIN and not filling fast enough. Reserve recovery now respects measured buffer flow instead of treating smoothed export as the full demand at EMPTY. MAX still caps fill; other modes retain their controls.

- **[v1.17.3](https://github.com/TylzSomeone/corewatch/releases/tag/v1.17.3)** — Clickable alert counter and a paginated list of affected reactors, reasons, suggested checks, and OPEN REACTOR buttons. Resolved alerts clear automatically. Improved incomplete-assembly diagnostics.

- **[v1.17.2](https://github.com/TylzSomeone/corewatch/releases/tag/v1.17.2)** — Restored the full startup splash with an animated progress bar, version, and connection/setup messages. It appears once per launch for at least four seconds, regardless of reactor count.

- **[v1.17.1](https://github.com/TylzSomeone/corewatch/releases/tag/v1.17.1)** — Redesigned the steam-reactor dashboard with a thin teal history graph, steam/coolant gauges, a rod bar, and touch buttons. Updated INFO with steam graph and tank guidance.

- **[v1.17.0](https://github.com/TylzSomeone/corewatch/releases/tag/v1.17.0)** — Independent multi-reactor controllers, a shared monitor selector, names, per-reactor settings, connection isolation, and a manual steam-reactor page. Added a third INFO page and migration guidance.

- **[v1.16.4](https://github.com/TylzSomeone/corewatch/releases/tag/v1.16.4)** — Added read-only fuel and casing temperatures for Extreme Reactors.

- **[v1.16.3](https://github.com/TylzSomeone/corewatch/releases/tag/v1.16.3)** — Clarified that you reboot from the CC computer’s terminal. The update screen labels the active version **RUNNING**.
- **[v1.16.2](https://github.com/TylzSomeone/corewatch/releases/tag/v1.16.2)** — The dashboard’s **INFO** button becomes **UPDATE** when a newer release is available.
- **[v1.16.1](https://github.com/TylzSomeone/corewatch/releases/tag/v1.16.1)** — First GitHub release. Added GitHub update checks and on-demand installation.

See [GitHub Releases](https://github.com/TylzSomeone/corewatch/releases) for downloads and full release notes.

You may download and run Corewatch on your Minecraft server.
