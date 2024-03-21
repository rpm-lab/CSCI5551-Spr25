---
layout: page
title: Project 6
parent: Projects
nav_order: 1
---
 
# Project 6

## Disclaimer

<b> Please DO NOT distribute project material or solutions online (e.g. public GitHub repositories). We take violations of the honor code very seriously. </b>

## Overview
For this assignment, you will implement mobile manipulation using concepts you have learned and implemented in the previous sections: finite state machine, inverse kinematics, and rrt connect.

- Mobile manipulation in `kineval/kineval_mobile_manipulation.js`

## Instructions

1. <b>Start with your solutions to project 5</b>
    - Solutions to project 5 will be released on 3/24/2024 (Sun). You can also start from here.
    - You must download 4 updated files to add support for mobile manipulation: `home.html`, `kineval/kineval.js`, `kineval/kineval_mobile_manipulate.js`, and `worlds/world_mobile_manipulate.js` [Download](/CSCI5551-Spr24/assets/projects/P6/updated.zip)
    - You should see the red cube and blue goal bubble at `http://localhost:8000/home.html?world=worlds/world_mobile_manipulate.js`.

2. <b>Finite State Machine Controller</b>
        
    - `kineval.robotMobileManipulateIterate()` in `kineval/kineval_mobile_manipulate.js` is the only function you need to implement for this project.
        - This function is called every iteration of the simulation.
        - This function contains boilerplate code for recommended state definitions.
        - You should implement the contents of each state branch and transitions.
        - <b>Whenever the configuration of the robot changes, this function should return the configuration as an array.</b>
            - These configurations along with the state of the object will be used in the autograder.

    - The entire process is as follows:
        - Move near the cube using RRT connect in `kineval/kineval_rrt_connect.js`.
        - Move end effector onto the cube using inverse kinematics `kineval/kineval_inverse_kinematics.js`.
        - Grasp the cube using `kineval.graspObject()` in `kineval/kineval.js`.
        - Move near the goal bubble using RRT connect.
        - Move end effector onto the goal bubble using inverse kinematics.
        - Release the cube using `kineval.releaseObject()` in `kineval/kineval.js`.

3. <b>RRT Connect</b>
    
    - You will use RRT connect to move the robot to a configuration where it can pick up/release the object.

    - Initialize, iterate, and traverse RRT connect in the corresponding states in `kineval.robotMobileManipulateIterate()`.
        - To initialize, copy and modify from `kineval.robotRRTPlannerInit()`.
        - To iterate, call `robot_rrt_planner_iterate()`.
        - To traverse, copy and modify from `kineval.planMotionRRTConnect()`
        - Make sure you remove your trees and motion plans after you are done traversing the motion plan.
        - Determine the goal configuration using any heuristic you want (for example, on the object).

4. <b>Inverse Kinematics</b>

    - You will use inverse kinematics to move the end effector to the object and the goal bubble.
        - Look at `kineval.randomizeIKtrial()` for setting and checking the goal pose.
        - Call `kineval.iterateIK` to  move .

5. <b>Tips</b>

    - Autograder checks your `kineval.robotMobileManipulateIterate()` on 5 different scenarios.
    
    - <b>Whenever the configuration of the robot changes, this `kineval.robotMobileManipulateIterate()` should return the configuration as a 1d array (as used in RRT). When it finishes, it should return "complete". Otherwise, it should not return anything.</b>

    - `worlds/world_mobile_manipulate.js` contains a dictionary `objs`, which has origin, size, and color defined in `objs['red_cube']` and `objs['blue_bubble']`

    - If your implementation is getting <b>stuck at IK stages</b>, it's likely you are not traversing the motion plan correctly (hence, the robot just stays in the original location where it's impossible to reach the IK goal). Similarly to how you manually initialized RRT and called `robot_rrt_planner_iterate()`, you have to manually move the robot to the configurations defined in `kineval.motion_plan` instead of relying on `kineval.planMotionRRTConnect()` in kineval_rrt_connect.js. The autograder avoids calling `kineval.planMotionRRTConnect()` for clarity's sake to avoid duplicate calls to rrt methods, but I realize that this behavior is different from the GUI and apologize for the inconvenience.

    - Removing markers from the world: Each vertex in the trees has a `.geom` property  that can be removed from the scene (e.g. `scene.remove(vertex.geom)`)

6. <b>Submit your `kineval/kineval_mobile_manipulate.js` and `kineval/kineval_rrt_connect` </b>
    - The autograder is available at [https://cse-ag-csci5551.cse.umn.edu/](https://cse-ag-csci5551.cse.umn.edu/)

<video width="720" muted controls>
    <source src="/CSCI5551-Spr24/assets/projects/P6/mobile_manipulate_rerender.mp4" type="video/mp4">
</video>

## Deadline

This project is due on <b>Wednesday, March 27th at 11:59pm CT</b>.

## Grading

The project is worth a total of 10 points.