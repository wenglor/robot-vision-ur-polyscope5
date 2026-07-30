# wenglor robot vision URCap for UR Polyscope 5

**URCap version:** 1.2.0 · **Example programs:** 1.1.0

This repository documents the **wenglor robot vision** URCap for Universal Robots running Polyscope 5. The URCap connects the generic vision interface to wenglor Machine Vision Devices, adds installation nodes (connection, calibration) and program nodes (Change job, Detect objects, Get object pose, Detect target), and ships with two example robot programs — one per calibration case.

> NOTE
>
> This repository focuses exclusively on UR Polyscope 5 URCap-specific topics. For general robot vision information, please refer to the [wenglor robot vision manual](https://wenglor.github.io/robot-vision-generic-string/).

📖 **Full documentation** is available in the [online manual](https://wenglor.github.io/robot-vision-ur-polyscope5/)

---

## Table of Contents

- [Prerequisites](#prerequisites)
- [Installation](#installation)
- [UR Installation & Calibration](#ur-installation--calibration)
- [Robot Program](#robot-program)
- [Troubleshooting](#troubleshooting)
- [Support & Feedback](#support--feedback)

---

## Prerequisites

> Supported: UR **E-series** with Polyscope **5.22** or newer. The CB-series is **not** supported.

- A UR E-series robot with Polyscope 5.22+.
- **Real Time Data Exchange (RTDE)** enabled in the UR security settings.
- Robot and Machine Vision Device in the same network.
- A [B60](https://www.wenglor.com/en/Machine-Vision/Smart-Cameras-and-Vision-Sensors/Smart-Camera-B60/c/cxmCID221375) or [Machine Vision Controller (MVC)](https://www.wenglor.com/en/Machine-Vision/Machine-Vision-Controllers/c/cxmCID221381).
- A [uniVision](https://www.wenglor.com/en/Machine-Vision/Machine-Vision-Software/Image-Processing-Software-uniVision-3/c/cxmCID222459) job for calibration and object detection.

---

## Files

The [`sources`](sources) directory contains:

| File | Description |
| --- | --- |
| `URCap_wenglorRobotVision_1.2.0.urcap` | The wenglor robot vision URCap for Polyscope 5. |
| `Camera_on_robot_example_1.1.0.urp` | Example program for the camera-on-robot case. |
| `Camera_not_on_robot_example_1.1.0.urp` | Example program for the camera-not-on-robot case. |

---

## Installation

1. Get the latest URCap from this repository's own [`sources`](sources) directory (see [Files](#files) above), and copy it onto a freshly formatted USB stick.
2. Plug the USB stick into the UR Teach Panel, open the menu in the top right corner → **System → URCaps → +**.
3. Select the **"wenglor robot vision"** URCap file and **restart the robot**.
4. After the reboot, the URCap shows a green hook.
5. On the device website (Jobs → Robot Server), set the robot manufacturer to **UR Polyscope 5 URCap**.

---

## UR Installation & Calibration

Under **Installation → URCaps → "wenglor robot vision"**:

1. **Connection tab** — enter the device IP (default `192.168.100.1`) and port (default `6008`), then set the connection slider to on.
2. **Calibration options tab** — select camera on/not on robot, the ZVZJ calibration target size, the calibration job, and the number of poses (5–11).
3. **Set calibration poses tab** — set the calibration poses (for camera on robot, the first pose is also the detection pose).
4. **Calibration tab** — when the system status LED is green, start the calibration.

See the [User Configuration](https://wenglor.github.io/robot-vision-ur-polyscope5/2_0_user_configuration/) page for the full procedure and LED status meanings.

---

## Robot Program

In the **Program** tab, build the program from the URCaps nodes:

- **Change job** — load the detection job (e.g. `find_objects.u3p`).
- **Detect objects** — trigger a detection and fill the buffer (`we_num_objects`).
- **Get object pose** — read an object into `we_object_pose` / `we_shape_model` / `we_custom_value` / `we_pose_valid`.
- **Detect target** — detect the calibration target into `we_target_pose`; assign it to `w_ref_frame` with an Assignment node.

Each example program contains three subprograms: `single_detection`, `multi_detection`, and `update_reference_frame`. See the [Robot Program](https://wenglor.github.io/robot-vision-ur-polyscope5/3_0_robot_program/) page.

---

## Troubleshooting

- **No connection:** check IP/port, that both devices are in the same network, that RTDE is enabled, and that the robot server is active with **UR Polyscope 5 URCap** selected.
- **Cannot start calibration:** the Calibration tab LED must be green (connected + all poses set).
- **`w_ref_frame` lost after restart:** save the installation before shutdown.

See the [Troubleshooting](https://wenglor.github.io/robot-vision-ur-polyscope5/4_0_troubleshooting/) page for more.

---

## Support & Feedback

- **Bugs:** Please open a new Issue in the [GitHub Issues section](../../issues) if needed.
- **Feature Requests & Ideas:** Discuss suggestions in the Discussions → Ideas category under [GitHub Discussions](../../discussions).
