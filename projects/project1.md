---
layout: page
title: Project 1
parent: Projects
nav_order: 1
---
 
# Project 1

## Disclaimer

<b> Please DO NOT distribute project material or solutions online (e.g. public GitHub repositories). We take violations of the honor code very seriously. </b>

## Overview
For this assignment, you will implement depth-first search and breadth-first search in `project_pathplan/graph_search.js`.

## Instructions

1. <b>Environment Setup</b>
    - Download [kineval-stencil](/CSCI5551-Spr24/assets/projects/kineval-stencil.zip) and unzip it.
    - Open a terminal and execute `python -m http.server` in the root directory of the project to start an http server.
    - Open a browser and go to `http://0.0.0.0:8000/project_pathplan/search_canvas.html`.
    - Open the developer tools console (Ctrl+Shift+J in Chrome) to probe variables like `search_alg`, `q_start_config`, `q_goal_config`, or `search_iter_count`.

    <video width="720" muted controls>
        <source src="/CSCI5551-Spr24/assets/projects/P1/environment.mp4" type="video/mp4">
    </video>

2. <b>Depth-first Search and Breadth-first Search</b>

    - Implement the search algorithms in `project_pathplan/graph_search.js`.
    - `initSearchGraph()` initializes the search graph `G`
        - Add code under `// STENCIL: determine whether this graph node should be the start...`
    - `iterateGraphSearch()` performs 1 iteration of the search algorithm.
        - Add code under `// STENCIL: implement a single iteration of a graph search algorithm...`
        - If `search_alg=="depth-first"`, execute depth-first search, if `search_alg=="breadth-first"`, execute breadth-first search.
        - Return `"succeeded"` if the search algorithm has found a path from the start to the goal, `"failed"` if the search algorithm has determined that no path exists, and `"iterating"` if the search algorithm is still searching.
        - Use helper functions `testCollision()`, `drawHighlightedPathGraph()`, and `draw_2D_configuration()` defined in `project_pathplan/infrastructure.js`  and `project_pathplan/draw.js` to navigate and visualize the graph appropriately.
        - <b>Make sure you add nodes in E, W, S, N order to match the video and pass the autograder.</b>
        - <b>Make sure you set `search_iterate=false` after the search algorithm has finished.</b>
    - You only need to implement depth-first search and breadth-first search (not A-star, greedy best-first search, or min heap).
    - To execute, open a browser and go to `http://0.0.0.0:8000/project_pathplan/search_canvas.html?search_alg=depth-first?planning_scene=narrow1`
        <video width="720" muted controls>
            <source src="/CSCI5551-Spr24/assets/projects/P1/depth-first.mp4" type="video/mp4">
        </video>
        - To execute breadth-first search, replace `depth-first` with `breadth-first`.
        <video width="720" muted controls>
            <source src="/CSCI5551-Spr24/assets/projects/P1/breadth-first.mp4" type="video/mp4">
        </video>
        - To execute other environments, replace `narrow1` with `empty`, `misc`, `narrow2`, or `three_sections`
        - More details on parameters can be found in `initSearch()` inside `project_pathplan/infrastructure.js

3. <b>Submit your `project_pathplan/graph_search.js`</b>
    - The autograder is available at [https://cse-ag-csci5551.cse.umn.edu/](https://cse-ag-csci5551.cse.umn.edu/)

## Deadline

This project is due on <b>Wednesday, January 31st at 11:59pm CT</b>.

## Grading

The project is worth a total of 12 points.