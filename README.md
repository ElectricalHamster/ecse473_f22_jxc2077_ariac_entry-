# ecse473_f23_jxc2077_ariac_entry
### use `roslaunch ariac_entry entry.launch` to launch it.
project is based on the information available from the ARIAC website, https://bitbucket.org/osrf/ariac/wiki/2019/documentation

launch files:
ecse_473_ariac.launch
The ecse_473_ariac.launch file is to start the environment and ables the start of competition, it contains the needed information about using pockage ecse_473_ariac.
entry.launch
This launch file runs the ecse_473_ariac.launch that also starts the competition.

Main function:
The functionality will be to move the manipulator over each part in a bin and back using a call to the Action Server interface.

### We first create a Trigger object, then call it using a ServiceClient. if the serivce is started successfully, you  can see a ROS info saying:
###########
ROS_INFO("Competition service called successfully
But if it failed, it will be following information.
ROS_ERROR("Competition service call failed! Goodness Gracious!!");
ROS_WARN("Competition service returned failure:  xxx ");
the integer, service_call_succeeded is used to check whether this call is successful.
###########

### It works similarly to Trigger, expect the topic we service is /ariac/material_locations.The locations of the products are found using the 10 logical cameras. 
### One for each of the six bins, two for the agvs, and two for quality. We used 10 callback to get their information.

Joint trajectories define how the robot moves. A trajetory conists of seven positions per point.
 Each point is a location the arm moves towards a destination, making them waypoints. 
Each point beyond the initial point can be found using T matrixes.
it have one degree more than the return of ur_kinematics.

We  use inverse(ur_kinematics::inverse((double *)&T, (double *)&q);. 
This method uses a provided T-matrix and finds how the six joints of the UR10 robot arm can angle themselves to have the final joint

the "end effector" reach the desired location. 


