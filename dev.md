---
layout: default
---

*   [Project Overview](./)
*   **Development**
*   [Challenges](./challenges.html)
*   [PIO](./pio.html)
*   [Retrospective](./retrospective.html)

# Development

### Parts & Components
* Adafruit PCA9685 16-Channel 12-bit I2C PWM/Servo Driver
* Arducam Pico4ML microcontroller development board
* Adafruit Analog 2-axis Thumb Joystick with Select Button + Breakout Board/Nintendo Wii Nunchuck
* 5 DoF Robotic Arm
	* 6x PWM-controlled hobby servos (2x HiTek HS-755MG, 3x HiTek HS-422, 1x HiTek HS-85BB)
	* Lynxmotion aluminum servo brackets
* 6x 940nm infrared LEDs
* 5VDC 10A power supply

### Assembly

![Robot arm](https://lh5.googleusercontent.com/dU20yPL3OBUOsR3HzihWKGnepbufl5L8TTRtDnTCjuzLlUg07074AWy-E-jZwrj7L2w=w2400)
*Our fully assembled 5 DoF robotic arm.*

After assembly of the robot arm, we wired the RP2040 board to the PCA9685 PWM driver which, when attached to the servos, can enable robot arm control directly from the microcontroller. This entire system can be viewed as a simplified diagram shown below:

![Block Diagram](https://lh4.googleusercontent.com/CoI8FougGbT-_4wW_VYSaboWVYG-fQFY_oDHZggRQf_kRZNHJtiuRr9ZOZoKhb6XSKI=w2400)

### Development Environment

Software for the project was developed across both Windows and Mac using Visual Studio Code and CLion IDEs.

[Here's the link to our code repository](https://github.com/ese-519-team-lobster/ese-519-team-lobster.github.io).

The following libraries/repositories were used/adapted in our project:
* https://github.com/cgxeiji/CGx-InverseK (Inverse Kinematics)
* https://gist.github.com/lsalmon/fad583622c4bdcb93f0f5722792a143f (Wii Nunchuck I2C interface)
* https://github.com/adafruit/Adafruit-PWM-Servo-Driver-Library (PCA9685 I2C interface)
* https://github.com/ArduCAM/RPI-Pico-Cam (Interface with Pico4ML camera and display)

### Timeline

Our first objective was to see if we could gain manual control of the robot arm. We began by testing if we could control the servo motors using the RP2040 and I2C PWM Driver:

![Servo](https://lh5.googleusercontent.com/U8_vvg05aZB-cOp9JSwlBr7n7px_I7Jvlxtk2lWQTDgX-tYn9Ppiu_m7o7LxCTlkjpQ=w2400)
*A servo being spun back and forth using the PCA9685 PWM driver.*

![Arm Demo Keyboard](https://lh5.googleusercontent.com/AhFAR-Qwwq0bZ2qPYu0vXA7i-0z3Yqc50g6mGS_U73zvisVjcHAJ_yL6mfJTrLT1OYw=w2400)
*Controlling the robot arm servos with keyboard controls.*

We wanted to work on making it easier for the arm to move to a point in 3D space. To accomplish this, we used an inverse kinematics library and interfaced it with our system. User keyboard controls now adjusted the change in X, Y, Z of the end effector. This was made a bit more intuitive with joystick controls:

![Joystick](https://lh3.googleusercontent.com/C7k0l0GXlQKElq3hT0yXP2wi9SvC9t84EF6NMvtZtFooGwPQQLF9yhQpfqUi8FxqlXg=w2400)
*Joystick directional input being read by a laptop.*

The next step was to enable our Pico4ML camera to obtain image readings and design a point tracking system. The approach for point tracking was to identify the brightest pixel in the image as our target:

![IR](https://lh3.googleusercontent.com/cibq7c9PZ8FnJaFEJcIiUg-uElxZYtzKw1kPVkkUqeGy3lXAVYGqvMZ8YWbOzbHcQeM=w2400)
      &emsp;*IR reflector camera demo.*

A simplified sort of convolution was implemented whereby the grayscale color value of each pixel is added to the value of the surrounding pixels, generating a "score" matrix whose maximum-valued element corresponded to the pixel that is surrounded by the most other bright pixels. This lets the program find the "brightest" point while accounting for the sometimes large number of pixels which are the greatest possible value.

To ensure that the intended target was the brightest point in the image, several infrared LEDs were mounted around the image sensor to illuminate the scene. A section of retroreflective tape was attached to the target.

![Assembled Arm](/assets/img/20221230_005143_HDR.jpg)
    *Assembled arm, including 3d-printed bracket holding Pico4ML and IR LEDs*

![Point Track](https://lh4.googleusercontent.com/sZKe2Ak1Ej1h7iPsuSJMX8TGTbK5VRPDznB6qQIcrTnyrya2egzhLXjisf4foDYfkRY=w2400)
    *Point tracking camera demo.*

Our final objective was to have our end effector move toward the target depending on where it was located on the camera image feed:

![Arm Demo IR](https://lh5.googleusercontent.com/jf1kyKZGcyEObChra9Rf-8jbWqaJpnVGn5pHSCD9E_E7ALajbXQ4OfzRC57IbES0Ipk=w2400)
*The robot arm follows the reflective tape on the cube.*


This led to the final product that we showed off during demo day! The robot arm could be controlled by keyboard input, Wii Nunchuck, or by the camera input. Users are able to switch between the modes using the buttons on the Nunchuck.