# OmniHand 3 Lite S User Guide

[简体中文](omnihand_3_lite_guide_zh_cn.md)

## Login

![User login](pic/login_en.png)

The window title shows the ToolBox version, for example, `OmniHand-ToolBox v2.7.6`.

Use the language selector in the upper-right corner to switch between **简体中文** and **English**.

Click **Login** to enter the User main interface. Both the default username and password are `user`; no changes are required.

## Main Interface

After login, the main interface opens:

![User main interface](pic/h3l_s_user_main_window_en.png)

### Main Interface Layout

![Main interface layout](pic/h3l_s_user_main_window_layout_en.png)

The main interface has nine areas:

1. **Navigation:** Home, [System Log](#system-log), and [Settings](#settings).
2. **Connection and layout:** product, hand, and device selection; **Connect / Disconnect**; **Update** and **Enable / Disable**, which become available after connecting (see [Quick Connection and Device Status](#quick-connection-and-device-status) and [Firmware Update](#firmware-update)); and the display switches at the upper right (see [Display Switches](#display-switches)).
3. **Device status:** device information (see [Quick Connection and Device Status](#quick-connection-and-device-status)).
4. **Hand model:** a 3D preview that follows joint positions, with **Calibrate** and **Reset View** at the lower left (see [3D Hand Model](#3d-hand-model)).
5. **Control:** control modes, action library import/export, and joint parameter sliders (see [Joint Control](#joint-control)).
6. **Tactile distribution:** live tactile data for Thumb, Index, Middle, Ring, Pinky, and Palm; the polling status, interval, and **Log** controls are at the top (see [Tactile Distribution](#tactile-distribution) and [Polling and Joint Status Matrix](#polling-and-joint-status-matrix)).
7. **Joint status:** polling checkboxes and the status matrix (see [Polling and Joint Status Matrix](#polling-and-joint-status-matrix)).
8. **Curves:** live charts and chart controls (see [Real-Time Curves](#real-time-curves)).
9. **Action configuration:** Preset and Sequence tabs (see [Action Configuration](#action-configuration)).

After you turn on **Vision** in the **...** menu, an optional [Vision Tracking](#vision-tracking) area appears and replaces the joint sliders in the control column.

### Display Switches

![Display switches](pic/h3l_s_display_switch_en.png)

The **Control** and **Polling** buttons and the **...** menu are at the upper right. A highlighted switch means the corresponding area is visible; a dimmed switch means it is hidden.

- **Control:** show or hide area ⑤, the control column.
- **Polling:** turn polling on or off (see [Polling and Joint Status Matrix](#polling-and-joint-status-matrix)).

The **...** menu contains:

- **Curve:** show or hide area ⑧, the curve column.
- **Action:** show or hide area ⑨, action configuration.
- **Tactile:** show or hide area ⑥, tactile distribution. This switch also controls tactile acquisition.
- **Matrix:** expand or collapse the data rows in area ⑦. The position, current, temperature, and error polling checkboxes remain visible in the header.
- **Model:** show or hide area ④, the hand model.
- **Vision:** show or hide [Vision Tracking](#vision-tracking). While visible, it replaces the joint sliders in the [control column](#joint-control).

### Quick Connection and Device Status

![Quick connection](pic/h3l_s_quick_connection_en.png)

1. Connect the hand to the computer through a ZLG CAN or HCAN adapter, then power on the OmniHand. The recommended supply voltage is **24 V**.
2. Select a detected CAN FD adapter from the device dropdown. If it shows **No device found**, click **⟳** on the right to refresh the list.
3. Select the product and the left/right hand. This product appears as **OmniHand 3 Lite S** in the product dropdown.
4. Click **Connect**. After a successful handshake, the device information area displays the actual device details, and the green **Connect** button becomes a red **Disconnect** button. The **Update**, **Enable**, and **Disable** buttons also become available.

For RS485 or detailed connection settings, such as CAN adapter index, channel, serial port, and baud rate, open [Settings](#settings) from the navigation bar.

If the device dropdown still shows **No device found** after refreshing, check the CAN adapter or USB-to-RS485 adapter and its connection to the computer. ZLG CAN and HCAN are supported. SocketCAN is also supported on Ubuntu when the adapter's official SocketCAN driver is installed and the interface is configured for **1 Mbit/s arbitration at an 80% sample point and 5 Mbit/s data at a 75% sample point** (`1M@80% + 5M@75%`).

The following screenshot shows a successful connection:

![Device information after connection](pic/h3l_s_get_device_info_success_en.png)

- **Update:** open the [Firmware Update](#firmware-update) page.
- **Enable / Disable:** control whether the hand's motors respond to control commands. Disabled joints do not execute position commands.
- **Device information:** seven items are shown: model, firmware version, hardware version, supply voltage, degrees of freedom, device ID, and serial number.

When disconnected, the device information fields show **Not connected** in red:

![Disconnected device information](pic/h3l_s_disconnection_device_info_en.png)

If the CAN adapter is connected but communication with the hand fails, the fields show **Unavailable** in yellow. Check the hand's power supply, wiring, connectors, and pin assignments:

![Device information unavailable](pic/h3l_s_get_device_info_fail_en.png)

An abnormal CAN adapter connection may indicate that the adapter was unplugged or has a loose connection:

![Abnormal CAN adapter connection](pic/h3l_s_connection_device_abnormal_en.png)

### Polling and Joint Status Matrix

![Polling and joint status matrix](pic/h3l_s_poll_en.png)

**Polling:** enable periodic queries to the hand at the configured interval. Disabling it stops periodic queries, and the matrix retains the last values received.

**Interval (ms):** the polling interval, **300 ms** by default. Press **Enter** to apply a change. Shorter intervals increase bus load; the default is generally sufficient.

**Log:** continuously write polled data to a CSV file while enabled.

**View:** hover over this button to see the recording's full CSV path; click it to open the containing folder.

**Joint status matrix:** each row shows a joint's position, current (mA), temperature (℃), and error code. Fields show `--` when disconnected.

The position, current, temperature, and error checkboxes in the matrix header independently select which parameters are polled. The **Tactile** switch in the **...** menu controls both tactile visibility and whether tactile data is queried.

Click a parameter cell in the matrix to add a live chart for that joint and parameter (see [Real-Time Curves](#real-time-curves)).

### Real-Time Curves

![Real-time curves](pic/h3l_s_realtime_curve_en.png)

The toolbar at the top of the curve column provides these controls:

- **Time window:** choose the duration shown on the X axis, with options from 1 second to 5 minutes.
- **Pause All / Resume All:** pause or resume updates to all chart views.
- **Clear All:** clear the data in all charts.
- **Close All:** close all chart cards.
- **Add:** open the chart selection dialog, choose a joint and parameter, and add a chart. Available parameters include position, current, temperature, velocity, torque, and error. For tactile parameters, select a finger or palm region instead of a joint.

If polling is disabled or a parameter's checkbox is cleared, that polled data stops updating and its polling chart freezes.

When no charts are open, a prompt asks you to click a parameter in the matrix. Clicking a matrix cell also adds its chart.

Each chart card provides the following controls:

- **Drag:** the first of the three small controls on the left. It appears only in card mode; drag it to reorder chart cards.
- **Reset (R):** the second control on the left. Reset X/Y zoom and the view to their defaults. Shortcut: **Ctrl + R**.
- **Clear (X):** the third control on the left. Clear the chart's existing data and start plotting again.
- **Time window:** at the upper right of the card. It works like the column's time-window dropdown but affects only this chart. Its tooltip lists zoom and pan shortcuts.
- **Pause / Resume:** pause or resume updates to this chart view.
- **Maximize / Restore:** expand the chart to fill the window or return it to card mode.

Move the pointer over the target chart before using these shortcuts:

| Shortcut | Function |
| --- | --- |
| Ctrl + ↑ / ↓ | Zoom the Y axis in / out |
| Ctrl + → / ← | Zoom the X axis in / out |
| Ctrl + Shift + ↑ / ↓ | Pan vertically |
| Ctrl + Shift + ← / → | Pan horizontally while paused |
| Ctrl + R | Reset the view |

Click a legend to show or hide its series, and hover over the plot to inspect values. Pausing a chart freezes its view while acquisition continues; only turning off **Polling** stops periodic acquisition.

### Joint Control

![Joint control column](pic/h3l_s_control_en.png)

**Debounce:** set the interval in milliseconds at which slider changes are sent, reducing the CAN FD bus load caused by continuous input.

**Control mode:** this product supports position, position＋torque, and position＋velocity＋torque control.

| Mode | Command Parameters | Description |
| --- | --- | --- |
| Position | Motor encoder position, 0–4096 | Default mode; set the target joint position only |
| Position＋Torque | Position and torque current, 0–1000 mA | Limit joint torque current while controlling position; default current: 300 mA |
| Position＋Velocity＋Torque | Position, velocity (rpm), and torque current (mA) | Also specify motor speed; default speed: 8000 rpm |

**rad:** off and dimmed by default, meaning sliders and inputs use motor encoder values from 0 to 4096. When enabled and highlighted, they use joint angles in radians. Actions saved in this mode store radian angles.

**Action dropdown:** lists the custom actions available for the selected left/right hand. Selecting an action updates the sliders to its saved positions and immediately sends the action to the hand. The first entry, **None**, means no action is selected. To delete an action, right-click its row or click the **✕** shown on hover.

**Init:** return all joints to the initial positions captured when the device connected.

**Save:** save the current slider positions as a custom action; enter a name when prompted. Regardless of which hand is connected, saving keeps mirrored left/right versions of the action. The saved action then appears in the **Action dropdown** list. To export it to a file, use **Export**.

**Export:** export all custom actions in the library to a `.json` file (see [Action Files](#action-files)).

**Import:** read actions from a `.json` file and add them to the library. If names conflict, a confirmation dialog lists the actions that will be overwritten.

**Joint sliders:** each joint has a number and name, followed by parameter sliders, target-value inputs, and current feedback values. Drag a slider to control the joint, or type a target value and press **Enter** to send it.

### 3D Hand Model

![3D hand model](pic/h3l_s_3d_model_en.png)

After connection, the model follows the joints' current positions. Use the mouse to rotate, zoom, or pan the view. Turn off **Model** in the **...** menu when it is not needed to free space for the curve and tactile areas.

![Calibrate and Reset View](pic/h3l_s_3d_calibrate_en.png)

**Calibrate:** restore the physical hand and the model to the default pose.

**Reset View:** restore the default camera view.

### Tactile Distribution

![Tactile distribution](pic/h3l_s_tactile_raw_data_en.png)

The **Tactile** switch in the **...** menu is enabled and highlighted by default. While enabled, the tactile area displays live data. Turn it off to hide the area.

The display is arranged as follows:

- **Regional readings on the left:** show the total force in g for each of six regions: Thumb, Index, Middle, Ring, Pinky, and Palm. The color bar beside each value changes from blue to red as force increases, making contact regions easy to identify.
- **Dot matrix on the right:** show the measurement points of each region as a dot matrix.

Raw tactile cells display **point indices**; hover over a cell to see its value in g.

### Action Configuration

The action configuration area has two tabs: **Preset** and **Sequence**.

**Preset**

These are the fixed gestures built into the SDK, 18 in total: Open, OK, Heart, Thumbs Up, Side Fist, Front Fist, Prayer, Bi-Heart 1, Bi-Heart 2, Bi-Heart 3, Point, Bow, Wave, Number 1, Number 3, Number 4, Number 7, and Number 8. Click a button to move the hand to the corresponding pose. Built-in gestures cannot be edited.

When switching between gestures, the hand first returns joints 3 and 4 to an intermediate pose, pauses briefly, and then moves to the target gesture. This is normal.

![Preset gestures](pic/h3l_s_gesture_en.png)

**Sequence**

Combine actions into a sequence for repeated execution:

- **Add:** add an action card. Click the card's name to open its editor, select an action from the dropdown, and enter the interval after that action in milliseconds.
- **Log:** when highlighted, record runtime data to CSV during sequence playback.
- **View:** hover to see the recording's full CSV path; click to open its folder.
- **Times:** enter a repeat count, or select **∞** for continuous playback. The completed repeat count is shown beside it.
- **Import:** load an action sequence from a JSON file (see [Action Files](#action-files)).
- **Export:** save the current action sequence to a local JSON file.
- **Clear:** remove all action cards from the current sequence, avoiding the need to delete a long imported sequence one step at a time.
- **Play / Stop:** execute the steps in order or stop playback. The current step is shown beside the controls.

![Action sequence](pic/h3l_s_action_sequences_en.png)

### Action Files

**Action library file (JSON):** imported/exported through the control column; defines individual actions. Action names in these examples are preserved as identifiers, including Chinese names.

```json
{ 
    "actions": [
        {
            "hand_type": "left",
            "name": "OK",
            "pos_axis_1": 0,
            "pos_axis_2": 0.830054,
            "pos_axis_3": 0.523019,
            "pos_axis_4": 1.314238,
            "position_type": "rad"
        },
        {
            "hand_type": "right",
            "name": "OK",
            "pos_axis_1": 0,
            "pos_axis_2": 0.830054,
            "pos_axis_3": 0.523019,
            "pos_axis_4": 1.314238,
            "position_type": "rad"
        },
        {
            "hand_type": "left",
            "name": "Heart",
            "pos_axis_1": 1.396263,
            "pos_axis_2": 1.02504,
            "pos_axis_3": 0.570125,
            "pos_axis_4": 0.888175,
            "position_type": "rad"
        },
        {
            "hand_type": "right",
            "name": "Heart",
            "pos_axis_1": 1.396263,
            "pos_axis_2": 1.02504,
            "pos_axis_3": 0.570125,
            "pos_axis_4": 0.888175,
            "position_type": "rad"
        }
    ],
    "format": "omnihand-actions",
    "product_type": "OMNIHAND_3_LITE",
    "product_variant": "H3L_S",
    "version": 3
}
```

**Action sequence file (JSON):** imported/exported through the Action Sequence tab. Steps can use preset gestures, individual actions from the action library, or actions loaded from a local file.

```json
{
    "format": "omnihand-sequence",
    "product_type": "OMNIHAND_3_LITE",
    "sequence_name": "默认序列",
    "steps": [
        {
            "delay_ms": 1000,
            "gesture_id": 1,
            "name": "OK",
            "source": "preset"
        },
        {
            "delay_ms": 1000,
            "gesture_id": 11,
            "name": "Bow",
            "source": "preset"
        }
    ],
    "version": 2
}

```

### Vision Tracking

![Vision tracking](pic/h3l_s_vision_en.png)

Turn on **Vision** in the **...** menu to open this area. It replaces the joint sliders in the control column.

**Left / Right Hand:** choose which human hand to track.

**Camera dropdown:** select the camera to use.

**Recalibrate:** enter calibration mode. Match each pose demonstrated by the 3D model with the selected human hand, then click the highlighted step button to capture that pose and advance to the next step.

### Firmware Update

After connecting, click **Update** at the top of the window:

![Open firmware update](pic/h3l_s_update_firmware_en.png)

Click **Select** and choose the firmware file from a local folder. The update starts once the file is selected, and the page shows progress through Download, Request, Transfer, Finalize, Restart, and Complete:

![Select firmware](pic/h3l_s_update_firmware_2_en.png)

When progress reaches **100%** and the page shows **Update Complete** (the device has restarted and the connection is restored), click **Back** to return to the main interface:

![Firmware update complete](pic/h3l_s_update_firmware_3_en.png)

### System Log

![System log](pic/h3l_s_system_log_en.png)

- **Traffic:** enable this switch to display transmitted and received messages.
- **Save Log:** export the log.
- **Clear:** clear the displayed log in the screen.

### Settings

![Settings](pic/h3l_s_settings_en.png)

The top of the page has **Single hand** and **Dual hands** tabs, which are disabled while connected. For dual hand mode, see [Dual Hand Settings](#dual-hand-settings). The following describes single hand mode.

The settings page provides the full connection configuration:

- **Product:** select **OmniHand 3 Lite S**, the model name of this product in the software.
- **Hand:** select right or left.
- **Connection type:** ZLGCAN, HCAN (both CAN FD), or RS485. SocketCAN is also available on Linux. The parameter area changes with the selected connection type.
- **Connection parameters:** for CAN FD, set the adapter index and channel to match the USB-to-CAN FD adapter (defaults: `0 / 0`). For RS485, set the serial port and baud rate.
- **Connection switch:** connect or disconnect using the switch on the right. The adjacent status text indicates disconnected, connecting, connection failed, or connected.
- **CAN FD bus parameters:** the application applies the fixed values required by the communication protocol; no manual configuration is needed.

Once connected, the product, connection type, and connection parameters are disabled. Disconnect before changing them. The left/right hand selection remains available while connected.

You can also set the device ID to a value from **0x01 to 0x7F**, or restore the factory-default device ID.

Timing settings include:

- **Request interval:** the gap between successive requests (default 4 ms).
- **Receive timeout:** the maximum wait for a reply frame; the operation returns as soon as the reply is received (default 150 ms).
- **Send timeout:** the maximum time the underlying send or write operation may wait (default 100 ms).
- **Data refresh interval:** control how often the UI displays updated data (default 200 ms).
- **3D model refresh interval:** control how often the 3D model is updated (default 200 ms).

You can also open the configuration folder and the user data folder; **Change User Data Folder** moves where data is saved.

### Dual Hand Settings

![Dual hand settings](pic/h3l_s_settings_dual_en.png)

Select **Dual hands** at the top of the settings page first. Two groups, **Device 1** and **Device 2**, then appear. Each has its own product, hand, connection type, CAN index and channel, device ID, and timing settings. The CAN index must match the adapter that each device is connected to.

Each device also has a **Polling interval** (default 300 ms).

![Dual hand connected](pic/h3l_s_settings_dual_connected_en.png)

When both hands are connected, the switch on the right of each group shows **Connected** in green.

### Dual Hand Mode

After selecting **Dual hands** in [Dual Hand Settings](#dual-hand-settings), the main interface shows two devices.

![Dual hand main interface](pic/h3l_s_dual_main_window_en.png)

1. Two connection areas, **Device 1** and **Device 2**, appear at the top. Select the product (**OmniHand 3 Lite S**), hand, and CAN adapter for each.
2. Open a device dropdown to see the device numbers detected on the computer. **Select the device that matches each hand**: Device 1 and Device 2 correspond to the left and right hands you want to control. Choosing the wrong device swaps the control between the two hands.

![Select device](pic/h3l_s_dual_connection_en.png)

3. Click **Connect** for each device.

#### Dual Hand Layout

![Dual hand layout](pic/h3l_s_dual_layout_en.png)

After both hands connect, they are shown side by side. Each hand has:

- its own connection bar and device information at the top;
- its own control column;
- a 3D model (both models share the view; **Calibrate** and **Reset View** are at the bottom center);
- a row of tactile readings below the model (Thumb, Index, Middle, Ring, Little, and Palm);
- its own **Preset** and **Sequence** bar at the bottom.

The curve column on the right is shared by both hands.

#### More Menu

![More menu](pic/h3l_s_dual_more_menu_en.png)

The **Control** and **Polling** buttons and the **...** menu at the upper right work like the single-hand [Display Switches](#display-switches). In dual hand mode, the **...** menu contains **Curve**, **Action**, **Tactile**, and **Model**.

#### Adding Curves

![Add curve](pic/h3l_s_dual_curve_add_en.png)

When no curve is shown, the column displays "Click Add to select a curve". Click **Add** in the curve column. In the **Add Curve** dialog, choose:

- **Device:** Device 1 or Device 2, that is, which hand's curve to view.
- **Joint:** the joint of that device.
- **Parameter:** Position, Position (Cmd-Fb), Torque (mA) (Cmd-Fb), Speed (rpm) (Cmd-Fb), Current (mA), Temperature (℃), Error, or Tactile (g).

The curve is then added for that device.

#### Preset Actions

Each hand has its own preset action bar at the bottom of the window. Click each one independently; they do not affect each other. The gestures are the same as in single hand mode (see [Action Configuration](#action-configuration)).

#### Real-Time Curves

![Dual hand real-time curves](pic/h3l_s_dual_realtime_curve_en.png)

Both hands' curves can be viewed at the same time. In the chart names, **D1** and **D2** stand for Device 1 and Device 2, for example `D1-Joint1-Position`.

#### Action Sequence

![Dual hand action sequence](pic/h3l_s_dual_action_sequence_en.png)

Each hand has its own **Sequence** bar, so each hand can have its own sequence. Usage is the same as in single hand mode (see [Action Configuration](#action-configuration)).

#### Calibrate and Reset View

![Dual hand calibrate](pic/h3l_s_dual_3d_calibrate_en.png)

**Calibrate** and **Reset View** at the bottom center of the 3D area work the same as in single hand mode (see [3D Hand Model](#3d-hand-model)).
