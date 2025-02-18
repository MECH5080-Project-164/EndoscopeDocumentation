# Student Code

In `/home/pharos/students/endo_ws/` is a ROS2 workspace a package:
- `external_led_control`: A package containing a node controlling GPIO pins to change the mode of external Chassis LEDs.

The `external_led_control` package has a node that can be used to control the mode of the external LEDs on the chassis.
The node is called `led_controller` and it listens on the topic `/led_control_mode`. The topic accepts messages of type `std_msgs/msg/String` with the following values:
- `0`: Turn off the LEDs.
- `1`: Turn on the LEDs with 50% duty cycle.
- `2`: Turn on the LEDs with 80% duty cycle.
- `3`: Turn on the LEDs with 100% duty cycle.

For ease of use, in `/home/pharos/scripts` there are several convenience scripts that can be used to control the LEDs:
- `led_controller.sh`: this is used by the `led_controller` node to control the LEDs and should not be removed. It is used to set the GPIO pins and control the external LEDs and can also be used as a standalone script outside of a ROS2 environment.
- `send_led_control_mode.sh`: this script can be used to send messages to the `/led_control_mode` topic to control the LEDs. It accepts a single argument which is the mode to set the LEDs to (0, 1, 2, or 3).
- `leds_on_boot.sh`: this script is used in the `/home/pharos/.profile` file and flashes the external LEDs when the system boots up and logs in.
- `rs_start.sh`: this script launches the RealSense camera node with the correct configuration to have IMU enabled. Sometimes when the node starts, there is ROS `[WARN]` output related to `Hardware Notification: Motion Module Failure`. When this occurs, just stop the node and run the script again.
  - To validate that the IMU is running do `ros2 topic echo /camera/camera/accel/sample` and you should see the IMU data.
  - The same can be done for `ros2 topic echo /camera/camera/gyro/sample`.
