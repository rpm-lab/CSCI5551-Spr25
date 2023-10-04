---
layout: page
title: Project 2
parent: Projects
nav_order: 1
---
 
# Project 2

## Disclaimer

<b> Please DO NOT distribute project material or solutions online (e.g. public GitHub repositories). We take violations of the honor code very seriously. </b>

## Overview
The objective of this project is to implement a robot choreography system that executes a dance routine with a Finite State Machine controller over joint angle setpoints.

- Quaternion joint rotation in `kineval/kineval_quaternion.js` (for quaternion functions) and "kineval/kineval_forward_kinematics" (to add axis-angle joint rotation to existing kinematic traversal)
    - Joint limit enforcement in `kineval/kineval_controls.js`
    - Prismatic joint implementation in `kineval/kineval_forward_kinematics.js`

- Interactive base control vectors in `kineval/kineval_forward_kinematics.js`

- Pose setpoint controller in `kineval/kineval_servo_control.js`

- Dance FSM in `kineval/kineval_servo_control.js` (FSM controller) and "home.html" (dance setpoint initialization)

<!-- [Grad section only] Fetch rosbridge interface -->

## Instructions

1. <b>Download the project starter code</b>
    - [Project 2 starter code: P2.zip](/CSCI5551-Fall23-S2/assets/projects/P2/P2.zip)

2. <b>Unzip the starter code and copy paste your solutions to project 1</b>
    - Copy paste your existing implementation of `kineval/kineval_matrix.js,` `kineval/kineval_robot_init_joints.js,` and `kineval/kineval_forward_kinematics.js` into the project 2 folder.
    - Solutions to project 1 will be released on 10/04/2023 (Wed), 2 days after project 1 is due. You can also use the released `kineval/kineval_matrix.js,` `kineval/kineval_robot_init_joints.js,` and `kineval/kineval_forward_kinematics.js` files.

3. <b>Joint state and control in `kineval/kineval_quaternion.js` and `kineval/kineval_forward_kinematics.js`.</b>

    - Going beyond the joint properties you worked with in project 1, each joint of the robot now needs several additional properties for joint rotation and control. These joint properties for the current angle rotation (".angle"), applied control (".control"), and servo parameters (".servo") have already been created within the function kineval.initRobotJoints(). The joint's angle will be used to calculate a rotation about the joint's (normal) axis of rotation vector, specified in the ".axis" field. To complete an implementation of 3D rotation due to joint movement, you will need to first implement basic quaternion functions in `kineval/kineval_quaternion.js` then extend your FK implementation in `kineval/kineval_forward_kinematics.js` to account for the additional rotations.

    - If joint axis rotation is implemented correctly, you should be able to use the 'u' and 'i' keys to move the currently active joint. These keys respectively decrement and increment the ".control" field of the active joint. Through the function kineval.applyControls(), this control value effectively adds an angular displacement to the joint angle.

    <video width="720" muted controls>
        <source src="/CSCI5551-Fall23-S2/assets/projects/P2/joint_rotation.mp4" type="video/mp4">
    </video>

    - Your implementation should include 1. proper implementation of all joint types in the robot descriptions and 2. proper enforcement of joint limits for the robot descriptions. The urdf.js files for the Fetch and Baxter robots, included in the provided code stencil, contain joints with with various types that correspond to different types of motion:
        - continuous: rotation about the joint axis with no joint limits
        - revolute: rotation about the joint axis with joint limits
        - prismatic: translation along the joint axis with joint limits
        - fixed: no motion of the joint

4. <b>Interactive base movement controls in `kineval/kineval_forward_kinematics.js`</b>

    - The user interface also enables controlling the global position and orientation of the robot base. In addition to joint updates, the system update function kineval.applyControls() also updates the base state (in robot.origin) with respect to its controls (specified in robot.controls). With the support function kineval.handleUserInput(), the 'wasd' keys are purposed to move the robot on the ground plane, with 'q' and 'e' keys for lateral base movement. In order for these keys to behave properly, you will need to add code to update variables that store the heading and lateral directions of the robot base: robot_heading and robot_lateral. These vectors need to be computed within your FK implementation in `kineval/kineval_forward_kinematics.js` and stored as global variables. They express the directions of the robot base's z-axis and x-axis in the global frame, respectively. Each of these variables should be a homogeneous 3D vector stored as a 2D array.

    <video width="720" muted controls>
        <source src="/CSCI5551-Fall23-S2/assets/projects/P2/base_move.mp4" type="video/mp4">
    </video>

    - If robot_heading and robot_lateral are implemented properly, the robot should now be interactively controllable in the ground plane using the keys described in the previous paragraph.

5. <b>Pose setpoint controller in `kineval/kineval_servo_control.js`</b>
    - Once joint axis rotation is implemented, you will implement a proportional setpoint controller for the robot joints in function kineval.robotArmControllerSetpoint() within `kineval/kineval_servo_control.js`. The desired angle for a joint 'JointX' is stored in kineval.params.setpoint_target['JointX'] as a scalar by the FSM controller or keyboard input. The setpoint controller should take this desired angle, the joint's current angle (".angle"), and servo gains (specified in the ".servo" object) to set the control (".control") for each joint. All of these joint object properties are initialized in the function kineval.initRobotJoints() in `kineval/kineval_robot_init_joints.js`. Note that the "servo.d_gain" is not used in this assignment; it is for advanced extensions.

    - Once you have implemented the control function described above, you can enable the conroller by either holding down the 'o' key or selecting 'persist_pd' from the UI. With the controller enabled, the robot will attempt to reach the current setpoint. One setpoint is provided with the stencil code: the zero pose, where all joint angles are zero. Pressing the '0' key sets the current setpoint to the zero setpoint.

    - Besides the zero setpoint, up to 9 other arbitrary pose setpoints can be stored by KinEval (in kineval.setpoints) for pose control. You can edit kineval.setpoints in your code for testing and/or for the FSM controller (see below), but the current robot pose can also be interactively stored into the setpoint list by pressing "Shift+number_key" (e.g., "Shift+1" would store the current robot pose as setpoint 1). You can then select any of the stored setpoints to be the current control target by pressing one of the non-zero number keys [1-9] that corresponds to a previously-stored setpoint. At any time, the currently stored setpoints can be output to the console as JavaScript code using the JSON.stringify function for the setpoint object: "JSON.stringify(kineval.setpoints);". Once you have found the setpoints needed to implement your desired dance, this setpoint array can be included in your code as part of your dance controller.

    - Since you will need to implement your setpoint controller before your FSM controller, for additional testing of your setpoint controller, a "clock movement" FSM controller has been provided as the function setpointClockMovement() in `kineval/kineval_servo_control.js`. This function can be invoked by holding down the 'c' key or from the UI.

    <video width="720" muted controls>
        <source src="/CSCI5551-Fall23-S2/assets/projects/P2/clock.mp4" type="video/mp4">
    </video>

6. <b>FSM controller in `kineval/kineval_servo_control.js`</b>

    - Once your pose setpoint controller is working, an FSM controller should be implemented in the function kineval.setpointDanceSequence() in `kineval/kineval_servo_control.js`. The reference implementation switches between the pose setpoints in kineval.setpoints based on two additional pieces of data: an array of indices (kineval.params.dance_sequence_index) and the current pose index (kineval.params.dance_pose_index). kineval.params.dance_sequence_index will tell your FSM the order in which the setpoints in kineval.setpoints should be selected to be the control target. Note that using this convention allows you to easily select the same setpoint multiple times to produce repetition in your dance. kineval.params.dance_pose_index is used to keep track of the current index within the dance pose sequence.

    <video width="720" muted controls>
        <source src="/CSCI5551-Fall23-S2/assets/projects/P2/fsm_controller.mp4" type="video/mp4">
    </video>

7. <b>Submit your `kineval/kineval_quaternion.js,` `kineval/kineval_forward_kinematics.js,` and `kineval/kineval_servo_control.js` `kineval/kineval_controls.js` files for grading</b>
    - The autograder is available at [https://cse-ag-csci5551.cse.umn.edu/](https://cse-ag-csci5551.cse.umn.edu/)


## Deadline

This project is due on <b>Wednesday, October 11th at 11:59pm CT</b>.

## Grading

The project is worth a total of 10 points.