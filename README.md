# This is a README / notes documenting the development process

## Catkin workspace
This is a catkin workspace repository, e.g. `~/catkin_ws`.    

### WARNING
This catkin_ws repository is __NOT__ an appropriate setup.    
The setup of a catkin_ws should follow ROSwiki's explicit instructions.    

This workspace however, is an example to how your catkin workspace should look like.    
_Notes: It is almost guaranteed to have pathing errors this way. If using anyway, fix them accordingly in CMakeLists.txt, CMakeCache.txt and Makefile by replacing the correct absolute path when necessary._ 

### Setting up catkin workspace
Start by creating a catkin workspace: ```mkdir -p ~/catkin_ws/src```    
then, ```cd ~/catkin_ws/```   

Here, to initialise from scratch do as official ROSwiki suggests:    
```catkin_make```    

Or just clone and copy the __content__ of this repo into your `~/catkin_ws/`.    
One may require to do `catkin_make` at `catkin_ws` directory anyway (after fixing all the pathing errors).

### Plugins
In `catkin_ws/src/qutms_autonomous_gazebo/plugins` contains plugin source and build files.

To build from source again, do `cd ~/catkin_ws/src/qutms_autonomous_gazebo/plugins/build`    
Then, do `cmake ../` which builds the parent directory into this build folder.   
This action generates CMakeCache, shared object, other files and a Makefile.   
Run `make`.

This should complete the plugin compilation.

_Notes:_
During dev, the custom plugins (/QEV2/vel_cmd and /QEV2/turn_cmd) were not showing up in `rostopic list`.    
The problem was later found that a explicit path (absolute or relative) must be declared in our `.world` file, in the line where we 'attached' the plugin.   
For example, our plugin.cc file is in `qutms_autonomous_gazebo/plugins`.
In which contains plugin source file as well as its cmake build folder. 
The generated .so file will appear in this build folder. 
Hence our world file, when specifying the .so file, must at least have `build/xxx.so` in front to complete a relative pathing. 

### Nodes
All the nodes used in this simulation are placed under the `nodes/` folder.   

Edit the file.cc and CMakeLists accordingly.   
To compile, go to `~/catkin_ws/` and run `catkin_make`. 
This should generate a file.so in `~/catkin_ws/devel/lib/{package name}/file.so`

Run this file.so in another terminal once the simulation is fired and running, and you should be able to control the robot.

### Using Gazebo
Given a correct ROS installation, there should be a `.gazebo/` folder under root, i.e.:   
```~/.gazebo/```

In which, there should be a `models/` folder that we can place our models in by doing:   
```mkdir ~/.gazebo/models/QEV2```   
_Notes: the folder name must be 'QEV2' to align with ROS system_

Place our __`model.sdf`__ and __`model.config`__ within this folder. 

### Launching
Typically, the `.world` can be run by simply doing:    
```gazebo _file_.world```

However, we eventually will end up using `roslaunch` and other ROS related commands. And that's what this README is mostly about - launching using roslaunch. 

Given the Catkin workspace is set up correctly, and if you haven't already, do:   
```cd ~/catkin_ws```   
```source devel/setup.bash```   

This should allow ROS filesystem to work. 
So now we do:  
```roslaunch qutms_autonomous_gazebo test.launch```

This should launch gazebo with a ground plane and our QEV2 model.

### Running
By running roslaunch, a roscore will be automatically started and gazebo launched.

Open another terminal, check if custom plugins are working by typing `rostopic list`.    
You should see /QEV2/xxx topics.
If not, the plugins have not loaded properly.

If loaded, you can publish to these nodes to control the robot.
For example:     
```rostopic pub /QEV2/vel_cmd std_msgs/Float32 "data: 5.0"```

This actuates the rear wheels to move the car forward at 5.0 speed. 
Steering command (/QEV2/turn_cmd) is similar. 

### Using nodes
As there will be more and more nodes coming into play, another README is placed in the src/nodes folder. 

For details of how the nodes are used, check there. 

In short, roslaunch as mentioned above.
This should fire up a roscore, then you can manually start your generated executable nodes.  































