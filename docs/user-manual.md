# SkyDefender Simulations User Manual

This manual explains how to connect SkyDefender panels, configure DCS World, and use the application during normal flights.

## 1. Install or update the application

1. Open the [latest SkyDefender release](https://github.com/Szketya/SkyDefenderSimulationSoftware/releases/latest).
2. Download and run the `.exe` installer.
3. Launch **SkyDefender Simulations** normally from the Start menu or desktop shortcut.

Windows may ask for permission while installing. After installation, do not use **Run as administrator** for normal use. Different Windows accounts keep separate application settings.

The application downloads stable updates automatically and installs them after you fully exit SkyDefender. If you update manually, exit through **QUIT** or tray **Exit** before running the new installer.

## 2. Connect a panel

### Add a panel

1. Connect the panel to a USB port.
2. Open **COM PORT ASSIGNMENTS**.
3. Select **ADD NEW PORT**.
4. Select the panel's COM port, such as `COM5`.
5. Select the matching panel type.
6. Wait for the status icon to confirm the connection.

The selected panel type determines which DCS data is sent to that device. Do not select a similar-looking panel type unless it matches your hardware.

### Understand the row status

| Status | Meaning | What to do |
| --- | --- | --- |
| No icon | A COM port or panel type is not selected | Complete both selections |
| Clock | The selection is being opened or checked | Wait briefly |
| Checkmark | The port is open, the detected device matches when identification is available, and the assignment is saved | No action needed |
| Warning | The detected device may not match the selected panel type | Check the panel type |
| Broken link | The saved panel is unplugged or has a new COM number | Select its current COM port on the same row |
| X | Windows could not open the port | Check the tooltip and **SYSTEM LOG** |

The COM port list refreshes automatically. Saved assignments are kept when a panel is disconnected. If Windows gives the panel a new COM number, select the new number on the existing row.

## 3. Configure DCS World

### Select the DCS profile

In **DCS CONFIG**, select **SELECT "Saved Games\DCS"** and choose your DCS profile folder.

The normal profile is:

```text
C:\Users\<your name>\Saved Games\DCS
```

An older installation may still use:

```text
C:\Users\<your name>\Saved Games\DCS.openbeta
```

Select the profile folder—not `Scripts`. SkyDefender finds or creates the `Scripts` folder automatically.

Windows can relocate Saved Games or display a localized folder name. Use the folder picker and follow the status shown by SkyDefender. A custom profile location is accepted, but the application shows a warning so you can confirm it was intentional.

### Select the DCS World installation

The **SELECT "DCS World" INSTALL** button appears only when an assigned panel needs additional F-14 controls.

Select the main DCS World installation folder, for example:

```text
C:\Program Files\Eagle Dynamics\DCS World
```

Mi-24 and other non-F-14 panels do not require this folder.

### Apply the configuration

Select **APPLY DCS CONFIG** after choosing the required folders.

SkyDefender will:

- install or update its DCS export files under the selected profile;
- add its entry to `Export.lua` without removing other supported entries;
- install the additional controls required by assigned F-14 panels;
- show whether the configuration was applied successfully.

You normally need to apply the configuration only:

- during first setup;
- after changing the DCS profile;
- when SkyDefender reports that setup or repair is needed.

You do not need to apply it before every flight.

### Understand F-14 binding status

SkyDefender v1.0.0 no longer replaces the F-14 aircraft `default.lua` files.

| Status | Meaning | What to do |
| --- | --- | --- |
| F-14 bindings active | Current SkyDefender controls are installed | No action needed |
| Legacy F-14 bindings active | Controls from an older SkyDefender installation are still working | No action needed |
| F-14 bindings need setup or repair | Required controls are missing | Select **APPLY DCS CONFIG** |
| F-14 bindings not configured | A required folder or initial setup is missing | Select the DCS World installation, then apply the configuration |
| F-14 bindings not required | No assigned panel needs the F-14 controls | No action needed |

Legacy bindings remain supported. After a DCS update or repair restores the original F-14 files, SkyDefender can install the current control setup when needed.

### Optional automatic repair

**AUTO REPAIR DCS CONFIG** appears when an assigned panel needs F-14 controls. It is disabled by default.

When enabled, SkyDefender checks the DCS configuration and automatically restores changes that a DCS update safely removed. If the application reports that automatic repair is blocked, use the manual steps in [Troubleshooting](troubleshooting.md#f-14-bindings-need-setup-or-repair).

## 4. Optional startup settings

### Auto start with DCS World

Enable **AUTO START WITH DCS WORLD** if you want SkyDefender to launch when DCS World starts.

- The setting is disabled until a DCS profile is selected.
- It is off by default.
- Turning it off removes only the SkyDefender auto-start entry.
- Repeated DCS launches do not create multiple running copies of SkyDefender.

### Start in tray

Enable **START IN TRAY** if you want SkyDefender to start with its window hidden. This setting applies to manual and DCS launches and is off by default.

The tray is also used during normal operation:

- Closing or minimizing the window hides it while the panel bridge keeps running.
- Select the tray icon or **Open SkyDefender** to restore the window.
- Select tray **Exit** or the in-app **QUIT** button to stop SkyDefender completely.

Windows may show a notification when SkyDefender starts in the tray.

## 5. Normal operation

1. Start SkyDefender manually or enable **AUTO START WITH DCS WORLD**.
2. Check that each connected panel row shows a successful status.
3. Check **DCS CONFIG** for any setup or repair warning.
4. Start a mission in the matching DCS aircraft.
5. Leave SkyDefender running while you fly.

If you launch SkyDefender again while it is already running, the existing window opens instead of starting another panel bridge.

## 6. Mi-24 Weapon panel bindings

For the switch covers to work correctly, bind these buttons in DCS Controls:

| Function | Device | Button |
| --- | --- | --- |
| Emergency Release Launchers Switch | Weapon Panel | `JOY_BTN21` |
| Emergency Release Launchers Switch Cover | Weapon Panel | `JOY_BTN47` |
| Emergency Release Stores Switch | Weapon Panel | `JOY_BTN33` |
| Emergency Release Stores Switch Cover | Weapon Panel | `JOY_BTN46` |
| Explosion on Jettison Switch - OFF | Weapon Panel | `JOY_BTN45` |
| Explosion on Jettison Switch - ON | Weapon Panel | `JOY_BTN32` |
| Explosion on Jettison Switch Cover - UP/DOWN | Weapon Panel | `JOY_BTN42` |

## 7. Update panel firmware

Only update firmware when a SkyDefender release note or support instruction identifies an update for your exact panel.

1. Download the correct `.hex` file for the panel from the [`firmware hex`](../firmware%20hex/) folder.
2. Open **FIRMWARE UPDATE** in SkyDefender.
3. Select the panel's current COM port under **Target COM**.
4. Select **BROWSE** and choose the correct `.hex` file.
5. Select **FLASH** and wait for the result.

Do not disconnect the panel while flashing. After a successful update, Windows may assign a new COM number. If that happens, select the new COM number on the existing assignment row and confirm the successful status before flying.

No panel firmware update is required for SkyDefender v1.0.0.

## 8. System Log and support

The **SYSTEM LOG** shows connection events, DCS configuration results, warnings, and errors.

When reporting a problem, include:

- the panel model and selected panel type;
- the COM port shown in SkyDefender;
- the relevant **SYSTEM LOG** text;
- the DCS aircraft and profile in use;
- what you expected and what happened instead.

Support may also ask for a `logs.txt` file or a DCS log. Follow the requested path shown in the application logs, because its location can differ between Windows accounts.

For DCS export problems, support may request:

```text
Saved Games\DCS\Logs\SDSsocket.log
```

Use your actual DCS profile name and Saved Games location.

For common problems, see [Troubleshooting](troubleshooting.md).

## 9. Digital Kneeboard panel

The Digital Kneeboard uses Windows display settings and a DCS monitor configuration in addition to its USB button connection. Follow the separate [Digital Kneeboard setup guide](../Digital-Kneeboard-Setup.md).

## 10. Uninstall or remove auto-start

Before uninstalling SkyDefender, turn off **AUTO START WITH DCS WORLD** if it is enabled.

If SkyDefender was already uninstalled and DCS still tries to start it, remove this file from the profile you configured:

```text
Saved Games\DCS\Scripts\Hooks\SkyDefenderAutostart.lua
```

Use an older `DCS.openbeta` profile or your custom profile name when applicable. The uninstaller does not remove other DCS-side configuration files automatically.
