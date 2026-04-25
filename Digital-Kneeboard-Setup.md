# Digital Kneeboard Panel  
## DCS World Secondary Screen Setup Guide

This guide explains how to use the **Digital Kneeboard Panel** as a secondary monitor in **DCS World**, and how to move the built-in DCS kneeboard onto that screen.

The recommended setup does **not** modify DCS core files, so it is the safest method for multiplayer **Integrity Check** compatibility.

---

## 1. Recommended Setup

Use this setup for normal use:

1. Connect the kneeboard panel.
2. Set the panel as an extended secondary display in Windows.
3. Create a custom DCS `MonitorSetup.lua` file in `Saved Games`.
4. Set DCS to use the combined multi-monitor resolution.
5. Open the built-in DCS kneeboard.
6. Drag and resize the kneeboard onto the secondary screen.
7. Bind the panel buttons in DCS Controls.

---

## 2. Integrity Check Compatibility

| Method | Description | Integrity Check |
|---|---|---|
| Recommended method | Windows extended display + `MonitorSetup.lua` in Saved Games + manually moved built-in kneeboard | Recommended |
| Core Lua modification | Editing files such as `ViewportHandling.lua` to force a fixed kneeboard position |  may fail IC |
| Kneeboard position mods | User mods that automatically reposition the DCS kneeboard | May fail IC, depending on modified files |
| OpenKneeboard | External kneeboard application | Usually IC-friendly, but not the same as the built-in DCS kneeboard |

Editing DCS core files such as:

```txt
DCS World\Scripts\Aircrafts\_Common\Cockpit\ViewportHandling.lua
```

is not recommended for normal users, because it may fail multiplayer Integrity Check and can be overwritten by DCS updates.

---

## 3. Panel Connections

The panel has three connectors:

### HDMI

Connect the HDMI cable to the PC.

For desktop PCs, connect it to the **graphics card HDMI output**, not the motherboard HDMI port.

### P — Power

The `P` connector powers the display.

It can be connected to:

- a PC USB port,
- a powered USB hub,
- a USB wall charger.

Required power:

```txt
5V USB power, minimum 1A
```

### D — Data

The `D` connector must be connected to the PC.

This connection is used for the physical panel buttons.

Without the `D` cable:

- the screen can still work,
- but the buttons will not work in DCS.

---

## 4. Windows Secondary Screen Setup

1. Right-click on the Windows desktop.
2. Open **Display settings**.
3. Click **Identify** to see which display is the kneeboard panel.
4. Select the kneeboard display.
5. Under **Multiple displays**, choose:

```txt
Extend desktop to this display
```

6. Make sure your main monitor is set as:

```txt
Make this my main display
```

7. Arrange the displays like this:

```txt
[ Main monitor ][ Kneeboard display ]
```

The kneeboard display should be on the **right side** of the main monitor.

Recommended settings:

```txt
Display scaling: 100%
Display mode: Extended desktop
```

Set the display orientation as needed:

| Panel position | Windows orientation |
|---|---|
| Horizontal panel | Landscape |
| Vertical panel | Portrait |

For a simple setup, keep the top edges or bottom edges of both screens aligned in Windows Display Settings.

---

## 5. Calculate the DCS Resolution

DCS must use the combined resolution of both screens.

Example:

```txt
Main monitor:       1920 x 1080
Kneeboard display:  1024 x 600
```

Combined DCS resolution:

```txt
1920 + 1024 = 2944 width
1080 height

DCS resolution = 2944 x 1080
```

Common examples:

| Main monitor | Kneeboard screen | DCS resolution |
|---|---:|---:|
| 1920×1080 | 800×480 | 2720×1080 |
| 1920×1080 | 1024×600 | 2944×1080 |
| 2560×1440 | 800×480 | 3360×1440 |
| 2560×1440 | 1024×600 | 3584×1440 |

---

## 6. Create the DCS MonitorSetup File

Open this folder:

```txt
C:\Users\<Your Windows User Name>\Saved Games\DCS\Config\
```

If you use DCS Open Beta, the folder may be:

```txt
C:\Users\<Your Windows User Name>\Saved Games\DCS.openbeta\Config\
```

Inside it, create this folder if it does not already exist:

```txt
MonitorSetup
```

The final path should be:

```txt
C:\Users\<Your Windows User Name>\Saved Games\DCS\Config\MonitorSetup\
```

Create a new file named:

```txt
SkyDefender_Kneeboard_Right.lua
```

---

## 7. MonitorSetup Example — 1920×1080 Main Monitor

Use this version if your main monitor is `1920×1080`:

```lua
_ = function(p) return p; end;
name = _('SkyDefender Kneeboard Right');
Description = 'Main monitor with right-side secondary kneeboard display';

Viewports =
{
    Center =
    {
        x = 0;
        y = 0;
        width = 1920;
        height = 1080;
        viewDx = 0;
        viewDy = 0;
        aspect = 1920 / 1080;
    }
}

GU_MAIN_VIEWPORT =
{
    x = 0;
    y = 0;
    width = 1920;
    height = 1080;
}

UIMainView = GU_MAIN_VIEWPORT
```

---

## 8. MonitorSetup Example — 2560×1440 Main Monitor

Use this version if your main monitor is `2560×1440`:

```lua
_ = function(p) return p; end;
name = _('SkyDefender Kneeboard Right');
Description = 'Main monitor with right-side secondary kneeboard display';

Viewports =
{
    Center =
    {
        x = 0;
        y = 0;
        width = 2560;
        height = 1440;
        viewDx = 0;
        viewDy = 0;
        aspect = 2560 / 1440;
    }
}

GU_MAIN_VIEWPORT =
{
    x = 0;
    y = 0;
    width = 2560;
    height = 1440;
}

UIMainView = GU_MAIN_VIEWPORT
```

> **Do not set the `Center` viewport to the full combined resolution.**  
> The `Center` viewport must only use the main monitor resolution.

---

## 9. Configure DCS

Start DCS World and open:

```txt
Options → System
```

Set the following options:

### Resolution

Enter the combined resolution.

Example for:

```txt
Main monitor:       1920 x 1080
Kneeboard display:  1024 x 600
```

Use:

```txt
2944x1080
```

### Monitors

Select:

```txt
SkyDefender Kneeboard Right
```

### Full Screen

Set:

```txt
OFF
```

For multi-monitor setups, DCS should run in borderless/windowed multi-monitor mode rather than exclusive fullscreen.

Click **OK** and restart DCS if needed.

---

## 10. Move the Built-in DCS Kneeboard to the Panel

Start a mission.

Open the DCS kneeboard with:

```txt
Right Shift + K
```

Then:

1. Move the mouse over the upper area of the kneeboard.
2. Hold the left mouse button.
3. Drag the kneeboard to the secondary kneeboard display.
4. Resize it by dragging its edges or corners.

DCS usually remembers the kneeboard position, but this may reset after:

- DCS updates,
- display changes,
- resolution changes,
- monitor layout changes.

---

## 11. Bind the Hardware Buttons in DCS

Make sure the `D` data cable is connected to the PC.

In DCS, open:

```txt
Options → Controls
```

Select the aircraft or use the general controls category.

Search for:

```txt
kneeboard
```

Recommended bindings:

| Function | Typical DCS command |
|---|---|
| Show / hide kneeboard | Kneeboard ON/OFF |
| Next page | Kneeboard Next Page |
| Previous page | Kneeboard Previous Page |
| Mark position | Kneeboard Mark Position |
| Glance view | Kneeboard Glance View |

To bind a button:

1. Click the control cell for the kneeboard panel device.
2. Press the physical button on the panel.
3. Confirm the binding.
4. Repeat for the other buttons.

---

## 12. Troubleshooting

### The DCS image is stretched across both screens

Check that the custom monitor setup is selected:

```txt
Options → System → Monitors
```

Make sure the `Center` viewport only uses the main monitor resolution.

Correct example for a 1920×1080 main monitor:

```lua
width = 1920;
height = 1080;
```

Incorrect:

```lua
width = 2944;
height = 1080;
```

The combined resolution is used in the DCS **Resolution** setting, not inside the `Center` viewport.

---

### The kneeboard screen is black

Check the following:

- HDMI is connected.
- `P` power cable is connected.
- The power source provides 5V and at least 1A.
- Windows Display Settings shows the screen.
- Windows is set to **Extend**, not **Duplicate**.
- DCS resolution includes the secondary display width.

---

### The panel buttons do not work

Check the following:

- The `D` data cable is connected to the PC.
- Windows detects the USB device.
- DCS Controls shows the device.
- The kneeboard commands are bound to the panel buttons.

---

### DCS menus are partly off-screen

Possible fixes:

1. Turn **Full Screen** off in DCS.
2. Check the total DCS resolution.
3. Check the Windows display arrangement.
4. Confirm that the correct monitor profile is selected.

If the DCS menu becomes unusable, reset the graphics settings by editing or deleting:

```txt
C:\Users\<Your Windows User Name>\Saved Games\DCS\Config\options.lua
```

For DCS Open Beta:

```txt
C:\Users\<Your Windows User Name>\Saved Games\DCS.openbeta\Config\options.lua
```

---

## 13. Alternative Methods

### Alternative 1 — Fixed Kneeboard Position by Lua Modification

Some users modify DCS Lua files to force the kneeboard to open at a fixed position.

Common file involved:

```txt
DCS World\Scripts\Aircrafts\_Common\Cockpit\ViewportHandling.lua
```

This can work, but it is not recommended for normal users.

Reasons:

- it modifies DCS core files,
- DCS updates can overwrite it,
- multiplayer servers may reject it with Integrity Check failure.

Use this only for single-player or controlled private environments.

---

### Alternative 2 — Kneeboard Position Mods

There are DCS user mods that automatically position the kneeboard for multi-monitor setups.

Some are distributed through the DCS User Files section and may require tools such as OvGME.

These can be convenient, but they are not the recommended default method because they may modify files checked by multiplayer Integrity Check.

---

### Alternative 3 — OpenKneeboard

OpenKneeboard is an external kneeboard application.

Advantages:

- useful for advanced kneeboard management,
- good for custom documents,
- does not require moving the built-in DCS kneeboard.

Limitations:

- it is not exactly the same as the built-in DCS kneeboard,
- it only displays image files from DCS kneeboard locations,
- Lua-generated kneeboard pages are not supported, including some built-in aircraft pages.

Use this if you want a separate advanced kneeboard system, not if you specifically want the original DCS kneeboard window.

---

## 14. Recommended Final Setup

For most users, use this setup:

### Hardware

- HDMI connected.
- `P` power connected to 5V / 1A USB power.
- `D` data connected to the PC.

### Windows

- Extended desktop enabled.
- Main monitor set as the primary display.
- Kneeboard screen placed to the right of the main monitor.
- Display scaling set to 100%.

### DCS

- Custom `MonitorSetup.lua` saved in `Saved Games`.
- Combined multi-monitor resolution selected.
- Full Screen set to OFF.
- `SkyDefender Kneeboard Right` monitor profile selected.

### In Mission

- Open the built-in DCS kneeboard.
- Drag and resize it onto the panel screen.
- Bind the panel buttons in DCS Controls.

This setup provides the cleanest result with the lowest risk of multiplayer Integrity Check problems.