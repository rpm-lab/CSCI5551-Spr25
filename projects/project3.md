---
layout: page
title: Project 3
parent: Projects
nav_order: 1
---
 
# Project 3

## Disclaimer

<b> Please DO NOT distribute project material or solutions online (e.g. public GitHub repositories). We take violations of the honor code very seriously. </b>

## Overview
For this assignment, you will now control your robot to reach to a given point in space through inverse kinematics for position control of the robot endeffector. Inverse kinematics will be implemented through gradient descent optimization with both the Jacobian Transpose and Jacobian Pseudoinverse methods, although only one will be invoked at run-time.

- Manipulator Jacobian in `kineval/kineval_inverse_kinematics.js`

- Gradient descent with Jacobian transpose in `kineval/kineval_inverse_kinematics.js`

- Jacobian pseudoinverse in `kineval/kineval_matrix.js` (pseudoinverse function) and `kineval/kineval_inverse_kinematics.js` (use in gradient descent)

## Instructions

1. <b>Download the project starter code</b>
    - [Project 3 starter code: P3.zip](/CSCI5551-Fall23-S2/assets/projects/P3/P3.zip)

2. <b>Start with your solutions to project 2</b>
    - Solutions to project 2 will be released on 10/13/2023 (Fri), 2 days after project 2 is due. You can also use the released solution as your starting point.

3. <b>Matrix pseudoinverse function in `kineval/kineval_matrix.js.`</b>

    - You will need to implement one additional matrix helper function in "kineval/kineval_matrix.js" for this assignment: matrix_pseudoinverse. This method will be necessary for the pseudoinverse version of gradient descent (see below). For this helper function, you are allowed to use a library function for matrix inversion, which can be invoked by using the provided routine numeric.inv(mat), available through numericjs.

4. <b>Core IK function in `kineval/kineval_inverse_kinematics.js`</b>

    - <b>Arguments</b>

        - endeffector_target_world: an object expressing the endeffector target in the world frame; it has two fields, endeffector_target_world.position, the target endeffector position (as a 3D homogeneous vector), and endeffector_target_world.orientation, the target endeffector orientation (as Euler angles)

        - endeffector_joint: the name of the joint directly connected to the endeffector

        - endeffector_position_local: the location of the endeffector in the local joint frame

    - <b>Expected Behavior</b> kineval.iterateIK() should compute controls for each joint. Upon update of the joints, these controls will move the configuration and endeffector of the robot closer to the target.

        <video width="720" muted controls>
            <source src="/CSCI5551-Fall23-S2/assets/projects/P3/inverse_kinematics.mp4" type="video/mp4">
        </video>

        - <b>Jacobian</b> Computation of the jacobian needs to only occur with joints along the <b>chain from the robot base (exclusive) to the endeffector joint (inclusive), not including fixed joints</b>.

        - <b>Position vs. Position + Orientation</b> The default IK behavior will be position-only endeffector control. Both endeffector position and orientation should be controlled when the boolean parameter <b>kineval.params.ik_orientation_included</b> is set to true, which can be done through the user interface (Inverse Kinematics->ik_orientation_included).

        <video width="720" muted controls>
            <source src="/CSCI5551-Fall23-S2/assets/projects/P3/inverse_kinematics_orientation.mp4" type="video/mp4">
        </video>

        - <b>Euler Angle Conversion</b> In order to handle the orientation of the endeffector in your IK implementation, you will need to calculate the orientation part of the error term, which will require you to implement a conversion from a rotation matrix to Euler angles. You may find an online reference to inform your implementation of this conversion or develop your own approach to the conversion calculation.

    - <b>Global Parameters</b> kineval.iterateIK() should also respect global parameters for using the Jacobian pseudoinverse (through boolean parameter <b>kineval.params.ik_pseudoinverse</b>) and step length of the IK iteration (through real-valued parameter <b>kineval.params.ik_steplength</b>). Note that these parameters can be changed through the user interface (under Inverse Kinematics). KinEval also maintains the current endeffector target information in the kineval.params.ik_target parameter.

    <video width="720" muted controls>
        <source src="/CSCI5551-Fall23-S2/assets/projects/P3/inverse_kinematics_pseudoinverse.mp4" type="video/mp4">
    </video>

    - <b>Usage</b> IK iterations can be invoked through the user interface (Inverse Kinematics->persist_ik) or by holding down the 'p' key. Further, the 'r'/'f' keys will move the target location up/down. You can also move the robot relative to the target using the robot base controls. When performing IK iterations, the endeffector and its target pose will be rendered as cube geometries in blue and green, respectively.

    - <b>Global Variables</b> you will need to set three global variables in kineval.iterateIK(): robot.dx, robot.jacobian, and robot.dq. There is a comment in "kineval/kineval_inverse_kinematics.js" that specifies what each of these variables should hold. Please note that robot.dx and robot.jacobian should both have six rows, even if you are doing position-only IK.

    - <b>Random Trials</b> You can also try running the random time trial to test the performance of your IK algorithm. This will not be part of the autograder/grading, but may help you debug. In general, IK with transpose does well when the arm is stretched far out, while IK with pseudoinverse does well when the arm is close to the body.

    <video width="720" muted controls>
        <source src="/CSCI5551-Fall23-S2/assets/projects/P3/inverse_kinematics_time.mp4" type="video/mp4">
    </video>


6. <b>Submit your `kineval/kineval_inverse_kinematics.js` and `kineval/kineval_matrix.js,
    - The autograder is available at [https://cse-ag-csci5551.cse.umn.edu/](https://cse-ag-csci5551.cse.umn.edu/)


## Deadline

This project is due on <b>Wednesday, October 25th at 11:59pm CT</b>.

## Grading

The project is worth a total of 10 points.