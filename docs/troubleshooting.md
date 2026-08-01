# SkyDefender Simulations Troubleshooting

Use the status icons and **SYSTEM LOG** first. They usually identify whether the problem is the USB connection, panel assignment, DCS profile, or F-14 configuration.

## A panel does not appear

1. Confirm that the panel has power and its USB data cable is connected.
2. Wait a few seconds for the COM port list to refresh automatically.
3. Disconnect and reconnect the panel.
4. Close any other application that may be using the same COM port.
5. Select **ADD NEW PORT** and check the list again.

If Windows does not show the panel as a COM device, reconnect it to another USB port and check whether its required USB driver is installed.

## A saved panel shows a broken-link status

Windows may assign a different COM number after reconnecting a panel or updating its firmware. The saved panel type is not lost.

Select the panel's current COM number on the existing row. You normally do not need to remove and recreate the assignment.

If several identical panels are connected, SkyDefender may ask you to choose manually rather than risk reconnecting the wrong hardware.

## The panel type shows a warning

The detected USB device may not match the selected panel type.

1. Confirm which physical panel is connected to that COM port.
2. Select the exact matching panel type.
3. If the panel is an older model that cannot be identified automatically, confirm the selection manually and check **SYSTEM LOG**.

## Windows cannot open the COM port

- Close serial monitors, firmware tools, or another copy of any application using the panel.
- Disconnect and reconnect the panel.
- Try another USB port.
- Restart SkyDefender.

If the row still shows an X status, copy the related **SYSTEM LOG** message for support.

## The DCS profile path shows a warning

Select the DCS profile folder under Windows Saved Games. The normal profile is:

```text
C:\Users\<your name>\Saved Games\DCS
```

An older installation may still use:

```text
C:\Users\<your name>\Saved Games\DCS.openbeta
```

Do not select the `Scripts` folder or the DCS World installation folder in this picker.

Windows may use a localized name for Saved Games or store it elsewhere. A warning is expected if you intentionally use a relocated or custom DCS profile; confirm that the chosen folder is the profile DCS actually uses.

## The DCS World installation selector is not shown

This is normal unless an assigned panel requires additional F-14 controls. Mi-24 and other non-F-14 panels do not need the DCS World installation folder.

Assign the correct F-14 panel type first. The installation selector then appears automatically.

## F-14 bindings need setup or repair

1. Confirm that both the DCS profile and DCS World installation folders are correct.
2. Select **APPLY DCS CONFIG**.
3. Check the F-14 bindings status again.

You can enable **AUTO REPAIR DCS CONFIG** to restore safe changes removed by later DCS updates.

If SkyDefender says automatic repair is blocked, run the official [DCS repair or cleanup procedure](https://www.digitalcombatsimulator.com/en/support/faq/repair/), then reopen SkyDefender and select **APPLY DCS CONFIG** again.

## Legacy F-14 bindings are active

No action is required. SkyDefender recognizes controls installed by older releases and leaves them working.

After a DCS update or repair restores the original F-14 files, SkyDefender may ask you to apply the current configuration. Follow the status shown in **DCS CONFIG**.

## A DCS update stops an F-14 panel from working

Open SkyDefender and check the F-14 bindings status.

- If setup or repair is needed, select **APPLY DCS CONFIG**.
- If automatic repair is enabled, bring the SkyDefender window into focus and allow it to recheck the configuration.
- If repair is blocked, follow the official DCS repair procedure linked above.

You do not need to replace or edit the F-14 `default.lua` files manually.

## A panel connects but does not react in DCS

1. Confirm that the assignment row shows a successful connection.
2. Confirm that the selected panel type matches the aircraft and physical panel.
3. Keep SkyDefender running while the mission is active.
4. Check **DCS CONFIG** and select **APPLY DCS CONFIG** if setup or repair is needed.
5. Restart DCS after applying configuration, then test again.

If the panel still does not react, send support the relevant **SYSTEM LOG** text and this DCS log:

```text
Saved Games\DCS\Logs\SDSsocket.log
```

Use your actual DCS profile name and Saved Games location.

## WinWing overwrites Export.lua

WinWing software may rewrite `Export.lua` after SkyDefender configuration. In WinWing, enable:

> Close the modification of Export.lua file

Then select **APPLY DCS CONFIG** again in SkyDefender.

## Older SkyDefender Lua files conflict

This may affect panels delivered before 2026-01-25 that used manually copied SkyDefender Lua files.

1. Open the configured DCS profile's `Scripts` folder.
2. Remove the old `SDS-socket.lua` and other old SkyDefender Lua files that were copied manually.
3. Select **APPLY DCS CONFIG** again.

Do not remove unrelated files belonging to other DCS applications.

## Auto start with DCS World cannot be enabled

Select the DCS profile first. The toggle remains disabled until SkyDefender knows which DCS profile to use.

If it is enabled but SkyDefender does not start:

1. Open SkyDefender normally—not with **Run as administrator**.
2. Turn **AUTO START WITH DCS WORLD** off and on again.
3. Start DCS World and check the SkyDefender tray icon.

## SkyDefender disappeared after closing or minimizing it

SkyDefender is still running in the Windows notification area so the panel bridge can continue working.

- Select the tray icon or **Open SkyDefender** to restore the window.
- Select tray **Exit** or the in-app **QUIT** button to stop it completely.

If **START IN TRAY** is enabled, the window is also hidden when SkyDefender first launches.

## Launching SkyDefender again does not create a new window

Only one copy runs at a time. A repeated launch should restore the existing window. If you still do not see it, check the Windows notification area and select the SkyDefender tray icon.

## Saved settings or panel assignments appear to be missing

Make sure you launched SkyDefender under the same Windows account as before and did not use **Run as administrator**. Administrator and normal launches can use different settings locations.

Then:

1. Exit completely using **QUIT** or tray **Exit**.
2. Launch SkyDefender normally.
3. Check whether the saved assignments return.
4. If not, copy the startup section of **SYSTEM LOG** and contact support.

## A firmware update fails

- Confirm that the selected COM port belongs to the panel being updated.
- Confirm that the `.hex` file is intended for that exact panel.
- Close other applications that may use the COM port.
- Do not disconnect the panel during the update.

After a successful flash, Windows may assign a new COM number. Select the new number on the existing assignment row.

## Information to send to support

Include:

- panel model and selected panel type;
- COM port;
- DCS aircraft and profile;
- relevant **SYSTEM LOG** text;
- the exact status or error message;
- steps that reproduce the problem.

Support may request additional `logs.txt` or DCS log files after reviewing this information.
