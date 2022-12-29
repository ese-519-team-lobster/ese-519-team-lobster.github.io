---
layout: default
---

*   [Project Overview](./)
*   [Development](./dev.html)
*   [Challenges](./challenges.html)
*   [PIO](./pio.html)
*   **Retrospective**

# Retrospective

One accomplishment that we found particularly satisfying was how well the camera point tracking worked after coding the logic.

Reflecting on our project design, there were a number of benefits and drawbacks with what we devised:

### Advantages

* PWM driver takes care of most of the complexity involved in controlling the joint servos.
* The camera we use for point tracking is already built into the Pico4ML. 
* Inverse Kinematics library was relatively straightforward to implement.
* Manual control and computer vision coding logic are very lightweight and simple, which is crucial for a microcontroller.

### Disadvantages

* The camera's small field of view makes it impossible to have the robot arm move toward any object located at any position within its reach. For the same reason, it's very easy for the system to lose track of a moving object unless it is almost directly underneath the arm.
* Servo motors are hobby servos, which are more prone to failure and cause a lot of jittering in the movement of the arm.
* Analog joystick has two axes and a button, which is not enough to control the three axes of the robot arm as well as the gripper.
* The robot arm only has five degrees of freedom, preventing some IK problems from being solvable and thus limiting the arm's workspace.


For the future, we would try to correct the downsides of our current system. First, we would replace the camera with one that has a larger FOV and mount it above the robot arm. Second, new and more expensive servos would be swapped in to increase the robustness of our arm and we'd be adding another servo for six degrees of freedom. Finally, we would consider more inputs (perhaps two joysticks and some buttons) to fully control the axes and the gripper. We would recommend a design with these improvements to future teams.

We would've liked to have evolved our logic to have the system accomplish a more complicated goal, like playing a legal game of checkers.

![Checkers](https://lh4.googleusercontent.com/Fszezl_1BwZ1SpxzaE6MF5N023FGDov6_vpj_1J6PFrCx1DCPlXnICWiYD5Git_8QRM=w2400)
*A robotic arm playing a game of checkers.*