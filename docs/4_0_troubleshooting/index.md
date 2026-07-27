# Troubleshooting

## URCap not installed / no green hook

- After adding the URCap under **System → URCaps → +**, you must **restart the robot**. The URCap only shows the green hook after a successful reboot.
- Use a **freshly formatted** USB stick for the URCap file.
- Confirm the robot is a UR **E-series** running Polyscope **5.22 or newer**. The CB-series is not supported.

## No connection to the Machine Vision Device

The **Connection** tab LED is red or the connection status is red:

- Check the cables and the network setup — the robot and the Machine Vision Device must be in the **same network**.
- Verify the IP address (default `192.168.100.1`) and port (default `6008`) in the **Connection** tab.
- Make sure **RTDE** (Real Time Data Exchange) is enabled in the UR security settings.
- Ensure the robot server on the device is active with **UR Polyscope 5 URCap** selected as the robot manufacturer (device website → Jobs → Robot Server). See [Settings on Device Website](https://wenglor.github.io/robot-vision-generic-string/4_0_robot_vision_server/4_2_0_settings_on_device_website/) in the wenglor robot vision manual.

## Processing Instance or Device Robot Vision status is red

- **Processing Instance red:** Check the status of the Processing Instance on the device website of the Machine Vision Device.
- **Device Robot Vision red:** There is no `Device Robot Vision` module in the current uniVision job. Add it to the job.

## Cannot start the calibration

Calibration can only be started when the **Calibration** tab system status LED is **green**:

| LED | What to do |
| --- | --- |
| 🔴 Red | Connect to the device **and** set all calibration poses. |
| 🟡 Yellow | Complete the missing condition — either connect to the device or finish setting all calibration poses. |
| 🟢 Green | Ready — start the calibration. |

## Calibration incomplete (camera not on robot)

- A yellow **Calibration** tab LED can mean the **second calibration step** is missing. For camera-not-on-robot, place the calibration plate on the object plane and trigger the second step (one image is captured). See [User Configuration → Camera not on robot](../2_0_user_configuration/index.md#camera-not-on-robot).
- Calculating the calibration results takes some time — wait until it completes.

## Insufficient calibration accuracy

- Use more than five calibration poses (seven to eleven give better results). Set the count in the **Calibration options** tab.
- Increase the variation between poses — the variance of the calibration *movements* matters more than the variance of the poses.
- Make sure the calibration plate covers as much of the camera image as possible and is fully visible.
- Prefer a wenglor ZVZJ calibration target and select the correct plate size.

For the general calibration guidelines, see the [Calibration Guidelines](https://wenglor.github.io/robot-vision-generic-string/4_0_robot_vision_server/4_1_calibration_guidelines/) in the wenglor robot vision manual.

## Detection pose issues (camera on robot)

- For camera on robot, the robot must be moved to the detection pose from the URCap, which is **identical to the first calibration pose**. To update it, set the detection pose on the URCap installation page and **re-run the calibration process**.

## `w_ref_frame` update is lost after restart

- `w_ref_frame` is saved in the **installation**, not in the program. **Save the installation** before shutting down the robot.
- Because the program reads installation feature values only at program start, an **Assignment node** is required to update `w_ref_frame` within the program run. See [UR Program → `update_reference_frame`](../3_0_robot_program/index.md#update_reference_frame).

## Error codes returned by the device

If the robot server returns a negative error code (`-5001` … `-5010`), it indicates a problem on the vision-device side. For the meaning of each code, see the [Generic Robot Vision Interface → Error codes](https://wenglor.github.io/robot-vision-generic-string/4_0_robot_vision_server/4_5_0_generic_robot_vision_interface/#error-codes) in the wenglor robot vision manual.
