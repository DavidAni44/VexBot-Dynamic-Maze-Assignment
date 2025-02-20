# Maze Exploration and Pathfinding Robot #
### Overview ###

This project involves controlling a robot to explore a maze, recording its path, and then retracing the shortest path from the goal back to the start. The robot uses a combination of sensors to detect obstacles and colour patterns and makes decisions based on the environment. After reaching the goal, the robot retraces its path and draws the maze in the console for visualization.

### Features ###
- Maze Exploration: The robot moves through the maze, recording its coordinates along the way.
- Path Retracing: Once the goal is reached, the robot reverses the recorded path to return to the start.
- Console Maze Visualization: The robot outputs the path it took in the console, marking the start and end points and the path taken.

### How It Works ###
- Initialization: The robot starts by turning 90 degrees to begin exploration. The initial coordinates are recorded.
- Exploration Loop: The robot moves forward and turns 90 degrees upon detecting an open space. It keeps track of its coordinates in a list.
- Goal Detection: When the robot detects the red color (using the down-facing eye sensor), it stops and begins retracing its path.
- Retracing: The robot reverses the recorded coordinates, using its location sensor to follow the path back to the starting point.
- Drawing the Path: The path is visualized in the console by drawing a grid with markers for the start, end, and path taken.
### Code Walkthrough ###
move(x_loc, y_loc): This function moves the robot to a specific (x, y) location by calculating the distance and turning to the appropriate angle.
draw_maze(coords_list): This function draws the maze in the console using the recorded coordinates.
main(): The main function handles the exploration and path retracing. It uses sensors to detect obstacles and the goal, and records the robot’s path.
