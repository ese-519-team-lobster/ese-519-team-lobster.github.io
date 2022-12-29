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
* Adafruit Analog 2-axis Thumb Joystick with Select Button + Breakout Board
* 5 DoF Robotic Arm
	* 6x PWM-controlled hobby Servos
	* Aluminum brackets

### Assembly

![Robot arm](https://lh5.googleusercontent.com/dU20yPL3OBUOsR3HzihWKGnepbufl5L8TTRtDnTCjuzLlUg07074AWy-E-jZwrj7L2w=w2400)
*Our fully assembled 5 DoF robotic arm.*

After assembly of the robot arm, we wired the RP2040 board to the PCA9685 PWM driver which, when attached to the servos, can enable robot arm control directly from the microcontroller. This entire system can be viewed as a simplified diagram shown below:

![Block Diagram](https://lh4.googleusercontent.com/CoI8FougGbT-_4wW_VYSaboWVYG-fQFY_oDHZggRQf_kRZNHJtiuRr9ZOZoKhb6XSKI=w2400)

### Development Environment

Software for the project was developed across both Windows and Mac using Visual Studio Code and CLion IDEs.

[Here's the link to our code repository](https://github.com/ndobrad/ese5190-final-project).

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

![Point Track](https://lh4.googleusercontent.com/sZKe2Ak1Ej1h7iPsuSJMX8TGTbK5VRPDznB6qQIcrTnyrya2egzhLXjisf4foDYfkRY=w2400)
    *Point tracking camera demo.*

Our final objective was to have our end effector move toward the target depending on where it was located on the camera image feed:

![Arm Demo IR](https://lh5.googleusercontent.com/jf1kyKZGcyEObChra9Rf-8jbWqaJpnVGn5pHSCD9E_E7ALajbXQ4OfzRC57IbES0Ipk=w2400)
*The robot arm follows the reflective tape on the cube.*

This led to the final product that we showed off during demo day!