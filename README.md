# Maze Exploration and Pathfinding Robot #
### Overview ###

This project involves controlling a robot to explore a maze, recording its path, and then retracing the shortest path from the goal back to the start. The robot uses sensors to detect obstacles and colour patterns and makes decisions based on the environment. After reaching the goal, the robot retraces its path and draws the maze in the console for visualization.

### Features ###
- Maze Exploration: The robot moves through the maze, recording its coordinates along the way.
- Path Retracing: Once the goal is reached, the robot reverses the recorded path to return to the start.
- Console Maze Visualization: The robot outputs the path it took in the console, marking the start and end points and the path taken.

### How It Works ###
- Initialization: The robot starts by turning 90 degrees to begin exploration. The initial coordinates are recorded.
- Exploration Loop: The robot moves forward and turns 90 degrees upon detecting an open space. It keeps track of its coordinates in a list.
- Goal Detection: When the robot detects the red colour (using the down-facing eye sensor), it stops and begins retracing its path.
- Retracing: The robot reverses the recorded coordinates, using its location sensor to follow the path back to the starting point.
- Drawing the Path: The path is visualized in the console by drawing a grid with markers for the start, end, and path taken.
  
### Code Walkthrough ###
- move(x_loc, y_loc): This function moves the robot to a specific (x, y) location by calculating the distance and turning to the appropriate angle.
- draw_maze(coords_list): This function draws the maze in the console using the recorded coordinates.
- main(): The main function handles the exploration and path retracing. It uses sensors to detect obstacles and the goal and records the robot’s path.

### Attempted Approach ###
Whilst working on this assignment I faced a few issues and attempted a range of different approaches including the Djinkstras algorithm, Depth First Search and Breadth-First Search, the reason I stuck with my more simple alogirthm was;
- The simplicity and ease of implementation
- The wall-following algorithm is more reactive as it makes decisions dynamically
- Doesn't rely on pre-mapped data

# See below for another attempt at algorithm trying to use BFS #
'''
        from vexcode import *
        import math
        from collections import deque
        
        
        DIRECTIONS = [(0, 250), (250, 0), (0, -250), (-250, 0)]
        
        visited = set()
        coordinates = []  # List to store coordinates in order
        
        
        def move_to(x_loc, y_loc):
            current_x = location.position(X, MM)
            current_y = location.position(Y, MM)
        
            dx = x_loc - current_x
            dy = y_loc - current_y
            
            if dx == 0 and dy == 0:
                return
        
            distance = (dx**2 + dy**2) ** 0.5
            angle = math.degrees(math.atan2(dy, dx))
        
            drivetrain.turn_to_heading(angle, DEGREES)
            drivetrain.drive_for(FORWARD, distance, MM)
        
        def wall_follow():
            global coordinates, visited
            while True:
                x = location.position(X, MM)
                y = location.position(Y, MM)
        
                if (x, y) not in visited:
                    coordinates.append((x, y))
                    visited.add((x, y))
        
                if down_eye.detect(RED):
                    break
        
                if left_eye.get_distance(MM) > 100:  # If left side is open, turn left
                    drivetrain.turn_for(LEFT, 90, DEGREES)
                    drivetrain.drive_for(FORWARD, 250, MM)
                elif front_distance.get_distance(MM) > 260:  # If path is clear, go forward
                    drivetrain.drive_for(FORWARD, 250, MM)
                else:  # Otherwise, turn right
                    drivetrain.turn_for(RIGHT, 90, DEGREES)
        
        def bfs_shortest_path(start, goal):
            queue = deque([(start, [])])
            visited_bfs = set()
            visited_bfs.add(start)
        
            while queue:
                (current, path) = queue.popleft()
        
                if current == goal:
                    return path
        
                for dx, dy in DIRECTIONS:
                    new_x, new_y = current[0] + dx, current[1] + dy
                    new_pos = (new_x, new_y)
        
                    if new_pos in visited and new_pos not in visited_bfs:
                        visited_bfs.add(new_pos)
                        queue.append((new_pos, path + [new_pos]))
        
            return [] 
        
        def backtrack(path):
            for x, y in path:
                move_to(x, y)
        
        
        def main():
            drivetrain.set_drive_velocity(100, PERCENT)
            drivetrain.set_turn_velocity(100, PERCENT)
        
            wall_follow()
        
        
            start = coordinates[0] 
            goal = coordinates[-1]
        
            shortest_path = bfs_shortest_path(goal, start)
        
            if shortest_path:
                backtrack(shortest_path)
        
            drivetrain.stop()
        
        vr_thread(main)
'''
