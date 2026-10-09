# 🛸 Project Tri-Spinner (A 3-Wheeled Omni ROS 2 Disaster)

> *"Why drive straight when you can unintentionally drift at a* $45^\circ$ *angle into your drywall?"*

Welcome to the official repository for my very first 3-wheeled omnidirectional robot powered by **ROS 2**. It has three wheels spaced at $120^\circ$, zero fear of collisions, and a strong tendency to turn living rooms and Gazebo worlds into low-budget Tokyo Drift scenes.

## 🛞 What Is This?

It's a holonomic robot platform! In theory, holonomic means:

* Moving in any direction instantaneously ($v_x, v_y$).
* Rotating independently ($\omega_z$).
* Looking cool and futuristic.

In practice, it means:

* The base vibrates so aggressively that screws loosen every 4 minutes.
* The inverse kinematics math works cleanly on paper, but one inverted sign sends the robot spinning into orbit.
* Carpet friction is our mortal enemy.

## 📐 Kinematics (Math vs. Reality)

The mathematical model says wheel velocities $\vec{v}_{wheels}$ are related to body velocity by:

$$
\begin{bmatrix} v_1 \\ v_2 \\ v_3 \end{bmatrix} = \begin{bmatrix} -\sin(\theta_1) & \cos(\theta_1) & L \\ -\sin(\theta_2) & \cos(\theta_2) & L \\ -\sin(\theta_3) & \cos(\theta_3) & L \end{bmatrix} \begin{bmatrix} v_x \\ v_y \\ \omega_z \end{bmatrix}
$$

What actually happens:

```
       Wheel 2 (120°)
          //
         /  \
        / 🤖 \
       //    \\
Wheel 1 (0°)   Wheel 3 (240°)

[Expected]: Smooth strafing left.
[Actual]:   Violent counter-clockwise corkscrew into the cat's water bowl.
```

## 🛠️ Hardware & Sim Stack

* **Brain:** Raspberry Pi / Micro-ROS microcontroller (or whatever Gazebo simulates without catching fire).
* **Motors:** 3x DC gearmotors with encoders (at least 1 encoder is probably lying).
* **Wheels:** 3x Omni wheels (famous for collecting dust bunnies and carpet fibers).
* **Power:** LiPo battery pack (please do not puncture).
* **Simulation:** Gazebo / RViz2 (where physics is suggested, not enforced).

## 📦 Prerequisites & Installation

Ensure you have ROS 2 installed (Humble / Iron / Jazzy recommended).

```bash
# 1. Source your ROS 2 environment
source /opt/ros/$ROS_DISTRO/setup.bash

# 2. Clone this repo into your workspace
cd ~/ros2_ws/src
git clone https://github.com/arjunkulkarni0208/omni3_wheel_bot.git

# 3. Resolve dependencies
cd ~/ros2_ws
rosdep install --from-paths src --ignore-src -r -y

# 4. Build and pray
colcon build --symlink-install
source install/setup.bash
```

## 🚀 Usage

### 1. Launching the Simulation

Fire up the simulation node:

```bash
ros2 launch omni3_wheel_bot launch_sim.launch.py
```

*Note: If Gazebo opens and your robot immediately launches into the stratosphere, that means the joint friction parameters need work.*

### 2. Driving with Teleop

In a separate terminal:

```bash
ros2 run teleop_twist_keyboard teleop_twist_keyboard
```

| Key | Expected Action | What Actually Happens |
| :--- | :--- | :--- |
| `i` | Drive Forward | Crawls forward while tilting suspiciously left |
| `,` | Reverse | Backs up; runs over its own virtual coordinate frame |
| `j` / `l` | Pure strafe | Wild spiral spin |
| `k` | Emergency Stop | Stops 0.4 seconds after clipping through a wall |

## 🪵 Known Bugs & Features

* [x] **Bug:** Robot drifts sideways when commanded to go dead straight.
  * *Fix:* Renamed behavior to "Autonomous Environmental Curiosity."
* [x] **Bug:** URDF wheels glitch into the floor plane.
  * *Status:* It's not a glitch, it's suspension testing.
* [ ] **TODO:** Calibrate wheel radius to decimal places instead of guessing.
* [ ] **TODO:** Clean hair out of the real-life omni rollers.
* [ ] **TODO:** Apologize to the living room baseboards.

## 📜 License

MIT License. You are free to copy, modify, and crash your own robot. No warranty provided for scuffed furniture.
