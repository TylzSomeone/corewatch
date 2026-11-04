# Corewatch

Corewatch is an in-game control panel for a direct-power Extreme Reactors reactor. It shows output history, stored energy, fuel, waste, and session efficiency. Choose Auto, Manual, Target RF/t, Standby, or Load Match from the touchscreen.

## Setup

Connect a Reinforced Reactor Computer Port to a CC: Tweaked computer directly or through enabled wired modems. Attach a wall of Advanced Monitors, ideally 4 blocks wide by 3 blocks tall. A CC: Tweaked Speaker is optional.

## Install

Run these commands on the CC computer. The server must allow CC: Tweaked HTTP downloads from GitHub.

```text
wget https://github.com/TylzSomeone/corewatch/releases/latest/download/corewatch corewatch
corewatch
```

Corewatch creates its own settings file. To run it automatically, add this line to your startup file.

```lua
shell.run("corewatch")
```

Open **INFO → UPDATES → CHECK** to look for a release. If one is available, tap **INSTALL** and reboot when ready. Use **BOOT CHECK** to opt into checks at startup.

You may download and run Corewatch on your Minecraft server.