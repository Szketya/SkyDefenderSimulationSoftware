# SkyDefender Simulations

SkyDefender Simulations is a desktop utility designed to connect **SkyDefender Simulations hardware panels** to **Digital Combat Simulator (DCS)** via serial (COM) and TCP communication.

The software acts as a bridge between:

- physical cockpit panels (USB serial devices)
- DCS Export.lua
- aircraft-specific DCS outout com port mappings

---

## Key Features

- Automatic COM port detection
- COM port to avionics-type assignment
- High-speed serial communication (230400 baud)
- Integrated TCP server for DCS Export.lua (port 5335)
- Safe and reversible DCS configuration installer
- Automatic update support
- Designed for SkyDefender Simulations hardware panels

---

## Supported Simulator

- **Digital Combat Simulator (DCS World)**
- Primary focus:
  - F-14 Tomcat
  - ARC-159 / ARC-182 / TACAN / AFCS / console panels

---

## Installation (End Users)

Download the latest stable version here:  
<https://github.com/Szketya/SkyDefenderSimulationSoftware/releases/latest>

1. Download the installer (.exe)
2. Run the installer (administrator rights recommended)
3. Launch SkyDefender Simulations
4. Configure COM ports and DCS paths

---

## Notes for Mi-24 Weapon Panel users

For the proper operation of the switch covers, you need to manually bind the following keys in DCS:

| Function                                     | Device       | Button    |
| -------------------------------------------- | ------------ | --------- |
| Emergency Release Launchers Switch           | Weapon Panel | JOY_BTN21 |
| Emergency Release Launchers Switch Cover     | Weapon Panel | JOY_BTN47 |
| Emergency Release Stores Switch              | Weapon Panel | JOY_BTN33 |
| Emergency Release Stores Switch Cover        | Weapon Panel | JOY_BTN46 |
| Explosion on Jettison Switch - OFF           | Weapon Panel | JOY_BTN45 |
| Explosion on Jettison Switch - ON            | Weapon Panel | JOY_BTN32 |
| Explosion on Jettison Switch Cover - UP/DOWN | Weapon Panel | JOY_BTN42 |

## DCS Integration Overview

SkyDefender Simulations automatically:

- installs Lua socket files into  
  Saved Games\DCS\Scripts
- safely patches or creates Export.lua
- installs a bundled default.lua into the F-14 keyboard input folder

No original DCS files are deleted.  
All overwritten files are backed up automatically.

---

### Important Notes (Existing Users / Compatibility)

#### Older SkyDefender Lua files (panels delivered before 2026-01-25)

If you received a SkyDefender panel before 2026-01-25 that worked with a previously provided Export.lua setup (e.g. ARC-159 / ARC-182 / TACAN / etc.), you must remove legacy Lua files to avoid conflicts.

Action required:

- Go to:  
  Saved Games\DCS\Scripts
- Delete older SkyDefender Lua files, especially:  
  SDS-socket.lua (and any other old SDS \*.lua you previously copied there)

Then re-apply configuration using APPLY DCS CONFIG in SkyDefender Simulations.

#### WinWing Export.lua protection

If you use WinWing software, ensure this option is enabled:

- “Close the modification of Export.lua file” = checked

This prevents WinWing from overwriting your Export.lua changes.

---

## Disclaimer

This project is not affiliated with Eagle Dynamics or Heatblur Simulations.  
All trademarks and copyrights belong to their respective owners.

---

## Author

SkyDefender Simulations

---

# USER MANUAL (End Users)

## 1. Application Startup

Launch SkyDefender Simulations.

On startup the application:

- starts a TCP server on port 5335
- scans the system for available COM ports

---

## 2. COM Port Management

### 2.1 Adding a Device

- Click ADD NEW PORT
- Select the correct COM port (e.g. COM5)
- The application identifies the connected device based on USB PID

### 2.2 Assigning a COM Type

Each COM port must be assigned a functional type, such as:

- ARC-159
- ARC-159 + TACAN
- ARC-182
- TACAN
- AFCS
- etc.

The selected type determines which DCS data is routed to that device.

### 2.3 Connection status (per row)

Each assignment row shows a **status icon** next to the port controls. Hover or click the icon for a short explanation.

| Icon             | Meaning                                                                                                                        |
| ---------------- | ------------------------------------------------------------------------------------------------------------------------------ |
| _(none)_         | No COM port or type selected yet                                                                                               |
| Clock            | Port and type selected; serial link not confirmed yet                                                                          |
| Checkmark        | Port open, USB identity matches the selected type, assignment saved                                                            |
| Warning triangle | Needs attention (e.g. USB type mismatch, or device not identifiable as a SkyDefender panel)                                    |
| Broken link      | Device was unplugged or the COM port changed; your **panel type assignment is kept** — select the new COM port in the dropdown |
| X                | Serial port could not be opened (see the tooltip and System Log)                                                               |

The COM port list **refreshes automatically** while the app is running. If a panel is unplugged and plugged back in (or Windows assigns a new COM number), update the port on the same row when prompted; you do not need to remove and re-add the assignment unless you want to.

---

## 3. DCS Configuration

### 3.1 Selecting Required Folders

Saved Games Scripts folder:  
PICK Saved Games\DCS\Scripts

Example:  
C:\Users\<username>\Saved Games\DCS\Scripts

DCS World folder:  
PICK Eagle Dynamics\DCS World folder

Example:  
C:\Program Files\Eagle Dynamics\DCS World

---

### 3.2 Applying Configuration

APPLY DCS CONFIG

The application will:

- copy SkyDefender Lua files into the Scripts directory
- create or update Export.lua
- create a backup of the original default.lua
- install the bundled F-14 keyboard mapping

---

### 3.3 When to use APPLY DCS CONFIG

The **APPLY DCS CONFIG** function does **not** need to be run every time.

It is recommended to run **APPLY DCS CONFIG** only in the following cases:

- After a **DCS World update**
- After a **SkyDefender Simulations software update**, especially if the update is applied before launching DCS

In normal operation, once the configuration has been applied successfully, no further action is required.

---

### 3.4 F-14 Keybind Availability (default.lua)

By default, **many cockpit controls of the F-14 are missing from the DCS Controls menu**.

SkyDefender Simulations installs a bundled **default.lua** file that restores missing keybinds required for proper operation of physical cockpit panels.

Current status:

- The default.lua currently includes:
  - **TACAN channel selector positions (Pilot seat only)**

Future updates:

- Upcoming SkyDefender Simulations updates will expand the default.lua to include:
  - all remaining missing F-14 keybinds
  - both pilot and RIO-related controls where applicable

This approach ensures full compatibility with physical switches and rotary selectors and allows the simulator to be operated as intended using real hardware.

---

## 4. Firmware Update

SkyDefender Simulations supports **firmware updates** for compatible hardware panels.

All SkyDefender Simulations panels are shipped with the **latest available firmware** at the time of delivery.  
When a new firmware update becomes available, it will be announced as part of a software release.

### Firmware availability and changelog

- The **latest release download page** always includes a **changelog**
- The changelog clearly states if a **new firmware version** is available for any specific panel
- The repository folder located next to `README.md` contains the available **.hex firmware files**
- Download the `.hex` file corresponding to the panel that received an update

### Firmware update procedure

1. Open **SkyDefender Simulations**
2. Navigate to the **Firmware Update** section
3. Select the correct **COM port**
   - Make sure the selected COM port belongs to the panel you want to update
4. Select the appropriate **.hex file** for the panel
5. Click **FLASH**

The firmware update will start automatically.

### After flashing

- In most cases, the panel will appear as a **new COM port**
- This is expected behavior

Required steps after update:

- Go to **COM PORT ASSIGNMENTS**
- On the existing row for that panel, select the **new COM port** from the dropdown (or add a row if you removed it earlier)
- Confirm the status icon shows OK before flying

The panel is now running the updated firmware and ready for use.

---

## 5. System Log

The SYSTEM LOG panel displays:

- COM port connection status
- DCS configuration results
- warnings and error messages

The log is human-readable and can be copied for troubleshooting.

---

## 6. Exiting the Application

QUIT

The application will:

- safely close all serial ports
- shut down cleanly

---

## 7. Common Issues

F-14 keyboard folder not found:

- The selected folder is not the DCS World root directory
- Verify that Mods\aircraft\F14 exists

No COM ports found:

- The device is not connected
- Required USB drivers are missing
- Wait a few seconds for the automatic port scan, or unplug and reconnect the panel

WinWing overwrites Export.lua:

- WinWing software may rewrite Export.lua after SkyDefender configuration
- Enable: “Close the modification of Export.lua file” in WinWing

Old SDS Lua files conflict (panels delivered before 2026-01-25):

- Remove legacy files from Saved Games\DCS\Scripts (especially SDS-socket.lua)
- Run APPLY DCS CONFIG again

---

## 8. Recommended Usage

- Start SkyDefender Simulations before launching DCS
- Do not run multiple instances simultaneously
- COM port assignments are saved automatically
- SkyDefender Simulations must remain running in the background while DCS is running (it provides the TCP bridge + COM routing). Do not close it after configuration.

---

## 9. Support Information

When reporting an issue, include:

- relevant SYSTEM LOG entries
- description of connected hardware
- log files for troubleshooting:
  - Saved Games\DCS\Logs\SDSsocket.log
  - the panel-specific log file(s) created by SkyDefender Simulations (attach all related ones)
