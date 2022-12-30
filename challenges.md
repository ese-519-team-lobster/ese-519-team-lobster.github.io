---
layout: default
---

*   [Project Overview](./)
*   [Development](./dev.html)
*   **Challenges**
*   [PIO](./pio.html)
*   [Retrospective](./retrospective.html)

# Challenges

Some major challenges we faced:

1. Communicating with the PWM Driver over I2C in C
   * Several times during development, the PCA9685 PWM driver ceased outputting the PWM signals that control the angle of the servo. Investigation with a logic analyzer did not reveal any problems with the I2C messages sent from the RP2040, and in fact showed that the PCA9685 was responding with the appropriate data when queried. Power-cycles and software resets were not effective in restoring function. When the PWM signals once again appeared, we were not able to determine the cause.
   
   ![I2C Trace](https://lh3.googleusercontent.com/hoIFnqj9BEzfcjZX9LKGdRvklaWo_pt5mOG4BhEWMUAntPOaibpuVgwWOYxpngwtuyk=w2400)
*A logic analyzer capture of I2C traffic and the generated PWM signal*

2. Smoothing of the robot arm's movements
   * The hobby servos used in the arm have only positional control inputs and no way to modify the speed at which the motor moves. This results in jerky, sudden motion from the arm when commanding a new position as all the motors move at their top speed to the new position. When combined with the relatively low framerate from the image sensor, the jerky movement introduced undamped oscillations to the arm's motion when seeking the object.
3. Camera's limited FOV
   * When the camera is mounted to the end effector, only a small portion of the work area is visible due to the low FOV. This requires manually navigating the arm until the target is within view before activating the point-tracking behavior.
4. Camera sensitivity
   * In bright environments, the IR LEDs do not provide enough illumination of the reflective target to differentiate it from the surroundings. A future improvement could be to use a visible-light filter to eliminate all light except the reflected infrared.
