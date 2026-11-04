# Corewatch

Corewatch is a touchscreen dashboard and controller for Extreme Reactors in Minecraft. See what your reactor is producing, what your base is drawing, and how much fuel you have left, all from one monitor wall.

![Corewatch dashboard showing power history, buffer, control rods, fuel, and waste](dashboard.png)

## What it does

- Graphs generation in RF/t and shows stored energy, net buffer change, and estimated RF out.
- Tracks fuel, estimated runtime, fuel efficiency, and waste.
- Compares energy, fuel burn, efficiency, and duty cycle across modes in **INFO → STATS**.
- Saves your buffer limits, RF/t target, boot mode, and sound preference.
- Reconnects when the reactor port returns and can check GitHub for updates.

## Control modes

| Mode | What it does |
| --- | --- |
| **Auto** | Adjusts the rods as the internal buffer fills. MIN is where throttling begins, and MAX is where the rods reach full insertion. |
| **Manual** | Holds rod position until you adjust it. Use the ±10% or ±1% buttons. |
| **Target RF/t** | Tracks an output you choose and backs off at MAX. Tap the RF/t setpoint to enter a number. |
| **Standby** | When armed, starts the reactor at or below MIN and shuts it off at MAX. DISARM shuts it down and disables automatic starts. |
| **Load Match** | Follows estimated demand to keep NET near zero. Below MIN it aims for a surplus, and MAX caps buffer fill. |

![Corewatch mode menu with Auto, Manual, Target RF/t, Standby, and Load Match](mode-menu.png)

Tap **MODE → BOOT MODE** to choose what opens after a reboot. Auto is the default. Standby boots disarmed. Tap **ARM** when you want it to manage starts. Tap the MIN and MAX values to enter them directly where those controls are available.

## Setup

- **Reactor:** An Extreme Reactors reactor that generates RF directly, with a **Reinforced Reactor Computer Port**. Steam-producing reactors and turbines are future work.
- **Computer:** A CC: Tweaked computer connected directly to the reactor port or through a wired modem network. Enable peripheral access on the wired modem attached to the port.
- **Display:** Advanced Monitors joined into a wall. **4 blocks wide by 3 blocks tall** is the recommended setup.
- **Sound:** Optional CC: Tweaked Speaker, connected directly or over the wired network. Toggle cues under **MODE**.

This setup was used on **All the Mods 10 v8.4**.

## Install

Run these commands in the CC computer's terminal. The server must allow CC: Tweaked HTTP downloads from GitHub.

```text
wget https://github.com/TylzSomeone/corewatch/releases/latest/download/corewatch corewatch
corewatch
```

Corewatch creates `corewatch-settings.txt` on first run. To launch automatically, add this line to your CC computer's `startup` file.

```lua
shell.run("corewatch")
```

## Updates

Open **INFO → UPDATES → CHECK**. Turn on **BOOT CHECK** if you want Corewatch to check each time it starts. When it finds a newer release, the dashboard's **INFO** button becomes **UPDATE** and opens the update screen.

Tap **INSTALL** when you're ready. Then **open the CC computer's terminal and hold Ctrl+R there**. The new version starts after reboot and keeps your saved settings.

## Troubleshooting

- **Reactor missing:** Run `peripherals` in the CC terminal. Check the cable and enable peripheral access on the modem attached to the Reinforced Reactor Computer Port.
- **Monitor missing:** Connect the Advanced Monitor wall directly or enable its wired modem. Use the 4×3 layout if text or controls look cramped.
- **Download or update fails:** Check whether CC: Tweaked HTTP is enabled and whether the server permits GitHub downloads. You can also download the `corewatch` file from Releases and copy it to the CC computer.
- **Standby waits after a reboot or a lost link:** Tap **ARM** to allow automatic starts again.

## Update log

- **[v1.16.4](https://github.com/TylzSomeone/corewatch/releases/tag/v1.16.4)** — Added read-only fuel and casing temperatures for Extreme Reactors.

- **[v1.16.3](https://github.com/TylzSomeone/corewatch/releases/tag/v1.16.3)** — Clarified that you reboot from the CC computer’s terminal. The update screen labels the active version **RUNNING**.
- **[v1.16.2](https://github.com/TylzSomeone/corewatch/releases/tag/v1.16.2)** — The dashboard’s **INFO** button becomes **UPDATE** when a newer release is available.
- **[v1.16.1](https://github.com/TylzSomeone/corewatch/releases/tag/v1.16.1)** — First GitHub release. Added GitHub update checks and on-demand installation.

See [GitHub Releases](https://github.com/TylzSomeone/corewatch/releases) for downloads and full release notes.

You may download and run Corewatch on your Minecraft server.
