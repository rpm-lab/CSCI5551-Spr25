---
layout: page
title: Project 2
parent: Projects
nav_order: 1
nav_exclude: false
---
 
# Project 2

## Disclaimer

<b> Please DO NOT distribute project material or solutions online (e.g. public GitHub repositories). We take violations of the honor code very seriously. </b>

## Overview
The objective of this project is to implement matrix operations, robot joint initializers, and forward kinematics in kineval-stencil.

- [Optional] Fill in stencils for Just Starting Mode in "kineval/kineval_startingpoint.js"

- Core matrix routines in "kineval/kineval_matrix.js"

- Joint selection/rendering, based on the kinematic hierarchy in "kineval/kineval_robot_init_joints.js"

- FK transforms in "kineval/kineval_forward_kinematics.js"

## Instructions

1. <b>Environment Setup</b>
    - Download [p2-stencil](/CSCI5551-Spr25/assets/projects/kinevalproject2.zip) and unzip it(the codebase will look much the same, but with regards to feedback we are trying to improve the documentation).
    - Open a terminal and execute `python -m http.server` in the root directory of the project to start an http server.

2. <b>Open `home.html` in Google Chrome</b>
    - Once unzipped, you should see files such as `home.html,` `kineval/kineval_matrix.js,` `kineval/kineval_robot_init_joints.js,` and `kineval/kineval_forward_kinematics.js`.
    - Install Python 3 and run `python -m http.server` in the project directory. Then open `http://localhost:8000/home.html` in Google Chrome. It should look like this:

    ![P2_home_html.png](/CSCI5551-Spr24/assets/projects/P2/P2_home_html.png)

3. <b>Implement the STENCIL sections in `kineval/kineval_matrix.js` except matrix_pesudoinverse and matrix_invert_affine.</b>

4. <b>Implement the STENCIL sections in `kineval/kineval_robot_init_joints.js`</b>
    - In `kineval.initRobotJoints()`, you should extend the robot object to complete the kinematic hierarchy to specify the parent and children joints for each link. The `.children` array of a link should be defined for all links except the leaves of the kinematic tree, in which case the `.children` property should be left undefined.
    - <b>KinEval refers to links and joints as strings, not pointers, within the robot object.</b> `robot.joints` (as well as `robot.links`) is an array of data objects that are indexed by strings. Each of these objects stores relevant fields of information about the joint, such as its transform (`.xform`), parent (`.parent`) and child (`.child`) in the kinematic hierarchy, local transform information (`.origin`), etc. As such, `robot.joints['JointX']` refers to an object for a joint. In contrast, `robot.joints['JointX'].child` refers to a string (`'LinkX'`), that can then be used to reference a link object (as `robot.links['LinkX']`). Similarly, `robot.links['LinkX'].parent` refers to a joint as a string `'JointX'` that can then then be used to reference a joint object in the `robot.joints` array.

5. <b>Implement the STENCIL sections in `kineval/kineval_forward_kinematics.js`</b>
    - `kineval.robotForwardKinematics()` is the entrypoint for your FK implementation. This function will need to call `kineval.buildFKTransforms()`, which is a function you will add to this file that updates matrix transforms for the frame of each link and joint with respect to the global world coordinates. The computed transform for each frame of the robot needs to be stored in the `.xform` field of each link or joint. For a given link named `'LinkX'`, this xform field can be accessed as `robot.links['LinkX'].xform`. For a given joint named `'JointX'`, this xform field can be accessed as `robot.joints['JointX'].xform`. Once `kineval.robotForwardKinematics()` completes, the updated transforms for each frame are used by the function `kineval.robotDraw()` in the support code to render the robot.
    - A matrix stack recursion can be used to compute these global frames, starting from the base of the robot (specified as a string in `robot.base`). This recursion should use the provided local translation and rotation parameters of each joint in relation to its parent link in its traversal of the hierarchy. For a given joint `'JointX'`, these translation and rotation parameters are stored in the robot object as `robot.joints['JointX'].origin.xyz` and `robot.joints['JointX'].origin.rpy`, respectively. The current global translation and rotation for the base of the robot (`robot.base`) in the world coordinate frame is stored in `robot.origin.xyz` and `robot.origin.rpy`, respectively.
    - To run your FK routine, you must toggle out of starting point mode. This toggle can be done interactively within the GUI menu or by setting `kineval.params.just_starting` to `false` in `home.html`.
    - ROS uses a different default coordinate system than threejs, which needs to be taken into account in the FK computation for these three robots. ROS assumes that the Z, X, and Y axes correspond to the up, forward, and side directions, respectively. In contrast, threejs assumes that the Y, Z, and X axes correspond to the up, forward, and side directions. The variable robot.links_geom_imported will be set to true when geometries have been imported from ROS and set to false when geometries are defined completely within the robot description file. You will need to extend your FK implementation to compensate for the coordinate frame difference when this variable is set to true.
    - You can test and degug your implementation by opening `home.html` with parameters attached to the back such as `?robot=robots/robot_mr2.js` `?robot=robots/robot_crawler.js` `?robot=robots/robot_urdf_example.js` `robots/fetch/fetch.urdf.js` `?robot=robots/sawyer/sawyer.urdf.js` `?robot=robots/baxter/baxter.urdf.js`. Your implementation should look like this:
    <br>![mr2.png](/CSCI5551-Spr24/assets/projects/P2/mr2.png) ![crawler.png](/CSCI5551-Spr24/assets/projects/P2/crawler.png) ![urdf.png](/CSCI5551-Spr24/assets/projects/P2/urdf.png) ![fetch.png](/CSCI5551-Spr24/assets/projects/P2/fetch.png) ![sawyer.png](/CSCI5551-Spr24/assets/projects/P2/sawyer.png) ![baxter.png](/CSCI5551-Spr24/assets/projects/P2/baxter.png)

6. <b>Submit your `kineval/kineval_matrix.js,` `kineval/kineval_robot_init_joints.js,` and `kineval/kineval_forward_kinematics.js` files for grading</b>
    - The autograder is available at [https://cse-ag-csci5551.cse.umn.edu/](https://cse-ag-csci5551.cse.umn.edu/)


## Deadline

This project is due on <b>Wednesday, February 12th at 11:59pm CT</b>.

## (Optional) Bonus Task
1. Implement the two functions "matrix_pseudoinverse()" and "matrix_invert_affine()" in "kineval/kineval_matrix.js"
2. Construct and display the model of SPOT robot from our lab in the provided window. The urdf files of the robot is given here ![spot.urdf](/CSCI5551-Spr25/assets/projects/P2/spot_urdf_model.zip). You may need to write your own js files based on the provided urdf files, instead of using them directly. 
## Grading

The project is worth a total of 10 points (The bonus tasks won't be graded, and no deadline will be applied as well. However, you are encouraged to demonstrate them to the instructors if you are interested in exploring more and completing them). 
