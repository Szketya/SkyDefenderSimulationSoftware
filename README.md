# SkyDefender Simulations

SkyDefender Simulations connects SkyDefender cockpit panels to DCS World on Windows. It manages panel connections, installs the required DCS configuration, and keeps your saved panel assignments between flights.

[Download the latest release](https://github.com/Szketya/SkyDefenderSimulationSoftware/releases/latest) · [User manual](docs/user-manual.md) · [Troubleshooting](docs/troubleshooting.md) · [Digital Kneeboard setup](Digital-Kneeboard-Setup.md)

## What the application does

- Detects connected SkyDefender panels and their Windows COM ports.
- Routes DCS cockpit data to each assigned panel.
- Installs and checks the required DCS files.
- Preserves panel assignments when a panel is unplugged or its COM number changes.
- Supports automatic updates and panel firmware updates.

## Supported panels

- F-14 ARC-159, ARC-182, TACAN, and radio combination panels
- F-14 left console, right vertical, and main panel sections
- Mi-24 Weapon panel
- SkyDefender Digital Kneeboard panel through its separate [DCS display setup guide](Digital-Kneeboard-Setup.md)

## Install or update

1. Open the [latest release](https://github.com/Szketya/SkyDefenderSimulationSoftware/releases/latest).
2. Download the SkyDefender Simulations `.exe` installer.
3. Run the installer. Windows may ask for permission to install the application.
4. Launch **SkyDefender Simulations** normally from the Start menu or desktop shortcut.

> Do not use **Run as administrator** for normal use. Running under a different Windows account can make saved settings appear to be missing.

Existing installations download stable updates automatically and install them after SkyDefender is fully exited.

## First setup

1. Connect your SkyDefender panel to the PC.
2. In **COM PORT ASSIGNMENTS**, select **ADD NEW PORT**.
3. Select the panel's COM port and the matching panel type.
4. Wait for the row status to confirm the connection.
5. In **DCS CONFIG**, select your DCS profile, normally `Saved Games\DCS`. Older installations may still use `Saved Games\DCS.openbeta`.
6. If you selected an F-14 panel, also select the DCS World installation folder when it appears.
7. Select **APPLY DCS CONFIG**.
8. Start DCS World and test the panel in the correct aircraft.

Select the DCS profile folder itself—not its `Scripts` folder. SkyDefender finds or creates `Scripts` automatically. Windows may display a localized name for Saved Games, and relocated or custom DCS profiles are supported.

For detailed instructions, see the [user manual](docs/user-manual.md).

## What is new in v1.0.0

- Clearer DCS profile selection with automatic folder creation and visible status.
- More update-resistant F-14 panel controls with optional automatic repair.
- Non-F-14 panels no longer require the DCS World installation folder.
- Optional **AUTO START WITH DCS WORLD** and **START IN TRAY** settings.
- More reliable loading of saved settings and panel assignments.
- A system tray icon for reopening or fully exiting the application.

All new startup and repair settings are optional and disabled by default. No panel firmware update is required for v1.0.0.

## Getting help

Start with [Troubleshooting](docs/troubleshooting.md). When contacting support, include:

- the panel model and selected panel type;
- the COM port shown in the application;
- the relevant text from **SYSTEM LOG**;
- what DCS aircraft and profile you use.

## Legal

See the repository [license](LICENSE) for the software and firmware distribution terms.

SkyDefender Simulations is an independent third-party manufacturer of flight simulator hardware and is not affiliated with, endorsed by, sponsored by, or approved by Eagle Dynamics, Heatblur Simulations, or any aircraft manufacturer.

DCS, DCS World, Eagle Dynamics, Heatblur Simulations, and all other trademarks, product names, and copyrights are the property of their respective owners. References are used only to indicate compatibility.

The SkyDefender Simulations name, logo, product photos, documentation, custom hardware designs, 3D models, and software are the property of SkyDefender Simulations unless otherwise stated.
