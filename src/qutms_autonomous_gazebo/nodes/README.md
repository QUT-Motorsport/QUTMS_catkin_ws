# Simple WASD controls
This node allows user to control the robot using WASD keys.

## Setup
The CMakeLists in this folder will be used by `catkin_make` when in `~/catkin_ws` directory.     
After `catkin_make` command, it should have generated an executable in `~/catkin_ws/devel/lib`.  


Start the simulation using roslaunch (where roscore is automatically fired up), then go into `~/catkin_ws/devel/lib` to locate generated executable and run it, i.e. `./qutms_autonomous_gazebo`. 

Now you should be able to control QEV2 using WASD keys.

## Controls
All control have latching effects - that is, they behave more like a toggle then a gradual acc/decceleration.

* W -> Forward at 10.0 speed
* S -> Backward at 10.0 speed
* E -> Reset to 0.0 speed (STOP)

* A -> Steer left at 3.0 angle
* D -> Steer right at 3.0 angle
* Q -> Reset steering angle to 0
