---
layout: page
title: Project 4
parent: Projects
nav_order: 1
---
 
# Project 4

## Disclaimer

<b> Please DO NOT distribute project material or solutions online (e.g. public GitHub repositories). We take violations of the honor code very seriously. </b>

## Overview
For this assignment, you will now implement a RRT-Connect motion planner to let your robot navigate from any configuration to the "zero configuration" (where every robot DOF has a zero value). This configuration space includes the state of each joint and the global orientation and position of the robot base.

- 2D RRT-Connect in `project_pathplan/rrt.js`

- Configuration space collision detection in `kineval/kineval_collision.js`

- Configuration space RRT-Connect in `kineval/kineval_rrt_connect.js`

## Instructions

1. <b>Start with your solutions to project 3</b>
    - Solutions to project 3 will be released on 11/01/2023 (Wed), 2 days after project 3 is due. You can also start from here.

2. <b>2D RRT-Connect in `project_pathplan/rrt.js`</b>
        
    - Change `initSearch()` in your `project_pathplan/infrastructure` to set `search_alg = "RRT-connect";` instead of `search_alg = "A-star";`

    - Complete the `iterateRRTConnect()` function. Its expected behavior is provided in the code stencil.

        - You do not need to implement `iterateRRT()` or `iterateRRTStar()`.

        - The two search tree global variables needed for RRT-Connect, `T_a` and `T_b`, are initialized for you in `project_pathplan/infrastructure.js`

        - You can use provided support functions from `project_pathplan/infrastructure.js`, including `insertTreeVertex()` and `insertTreeEdge()`

        - You may also create additional helper functions in `project_pathplan/rrt.js` to handle different steps of the RRT-Connect algorithm; some suggestions are provided in the code stencil

        - `iterateRRTConnect()` is called for you from the animation code, and it should perform just one iteration of the RRT-Connect algorithm each time it is called

        - You should use `drawHighlightedPath()`, not `drawHighlightedPathGraph()`, to visualize the final path found by RRT-Connect; see the implementation in `draw.js` for information about how this function works

    - You can check your implementation by opening `http://localhost:8000/project_pathplan/search_canvas.html` in your browser. It will look like the video below.

<video width="720" muted controls>
    <source src="/CSCI5551-Fall23-S2/assets/projects/P4/2d_rrt.mp4" type="video/mp4">
</video>


3. <b>Configuration space collision detection in `kineval/kineval_collision.js`</b>

    - Complete `kineval/kineval_collision.js`

        - Uncomment `return robot_collision_forward_kinematics(q);`

        - Implement `robot_collision_forward_kinematics()`, `traverse_collision_forward_kinematics_joint()` and any helper functions you need.

        - When finished, `kineval.poseIsCollision()` should return the name of the link in collision.
    
    - You can check your implementation by opening `http://localhost:8000/home.html` in your browser. The kineval code will automatically display the colliding link in red wireframes like the video below.

<video width="720" muted controls>
    <source src="/CSCI5551-Fall23-S2/assets/projects/P4/kineval_collision.mp4" type="video/mp4">
</video>

4. <b>Configuration space RRT-Connect in `kineval/kineval_rrt_connect.js`</b>

    - Modify `kineval.robotRRTPlannerInit()` to initialize RRT trees.

    - Complete `robot_rrt_planner_iterate()` and any helper functions in `kineval/kineval_rrt_connect.js`.

        - This function must execute a single RRT-Connect iteration.

        - Return `"reached"` if the search succeeds, and something not `"reached"` otherwise.

        - When the search succeeds, set the path `kineval.motion_plan` as a list of configurations from `q_start_configuration` to `q_goal_configuration`.

        - Your configuration space is constrained to robot base positions inside `robot_boundary`.

        - The robot cannot take steps longer than 1 (the 2-norm of the delta should be leq 1, analogous to eps=1 in 2D RRT).

    - When finished, open `http://localhost:8000/home.html?world=worlds/world_s.js`, move the robot to the opposite corner, press `x` to zoom out a bit, and press `m` to initiate the search. After the path is found, press `b` and `n` to move the robot through the found plan. It should look like the video below (Download and play this video if it freezes).

<video width="720" muted controls>
    <source src="/CSCI5551-Fall23-S2/assets/projects/P4/kineval_rrt.mp4" type="video/mp4">
</video>

5. <b>Submit your `project_pathplan/rrt.js`, `kineval/kineval_collision.js`, and `kineval/kineval_rrt_connect.js` </b>
    - The autograder is available at [https://cse-ag-csci5551.cse.umn.edu/](https://cse-ag-csci5551.cse.umn.edu/)
    <!-- - The autograder for `kineval/kineval_rrt_connect.js` is still under construction. Stay tuned for updates. -->


## Deadline

This project is due on <b>Wednesday, November 15th at 11:59pm CT</b>.

## Grading

The project is worth a total of 12 points.