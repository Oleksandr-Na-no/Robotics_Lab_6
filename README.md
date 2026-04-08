## How to Run Lab 6: Motion Planning for Mobile Robots (Nav2)

> Previous labs:
> [Lab 5](https://www.google.com/search?q=https://github.com/Oleksandr-Na-no/Robotics_Lab_5) 

-----

### 1\. Prepare the Environment & Docker

Open the Docker container from the **[robotics\_lpnu](https://github.com/RybOlya/robotics_lpnu/tree/master)** repository.

> ⚠️ **Note:** If this is your first time running Nav2, you must rebuild the Docker image to install the required packages.

```bash
cd robotics_lpnu/
./scripts/cmd build-docker
./scripts/cmd run
```

-----

### 2\. Build Workspace

Build the `lab6` package in your workspace:

```bash
source /opt/ros/jazzy/setup.bash
cd /opt/ws
colcon build --packages-select lab6
source install/setup.bash
```

-----

### 3\. Setup Environment Before Run

Before launching anything, make sure the environment is sourced:

```bash
cd /opt/ws
source install/setup.bash
source /opt/ros/jazzy/setup.bash
```

-----

### 4\. Running Lab 6: Nav2 Stack

This launch file starts Gazebo with the `room_nav2` world (8x8m room with obstacles), spawns the TurtleBot3, and brings up the Nav2 stack (map server, AMCL localization, planner, controller, and behavior tree).

**Launch simulation + Nav2:**

```bash
ros2 launch lab6 nav2_room_bringup.launch.py
```

-----

### 5\. Controlling the Robot via RViz

Once RViz and Gazebo are open, follow these steps to navigate:

1.  **Set the Frame:** Ensure the **Fixed Frame** is set to `map`.
2.  **Localize:** Click **2D Pose Estimate** in the top panel and set the robot's initial position and orientation to match what you see in Gazebo.
3.  **Navigate:** Click **Nav2 Goal** and select a target destination on the map. The robot will plan a global path and dynamically avoid obstacles using the local costmap.

-----

### 6\. Tuning Nav2 Parameters (Configuration)

The navigation parameters (velocities, costmap resolutions, inflations, goal tolerances) are heavily tuned for this run. If you need to adjust or experiment with them, edit the YAML file:

```bash
lab6/config/nav2_params.yaml
```

> ⚠️ **Important:** After making any changes to the YAML parameters, you must rebuild the package (Step 2) and restart the launch file (Step 4) for the new configurations to take effect.
