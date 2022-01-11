baxter_simulator
==============

Gazebo simulation with emulated interfaces for the Baxter Research Robot

Assume you have installed ROS noetic. To build from source, inside the catkin_ws run the following:

::
    
    sudo apt-get install python3-rosinstall
    source /opt/ros/noetic/setup.bash
    rosinstall ./src https://raw.githubusercontent.com/HaoguangYang/baxter_simulator/master/baxter_simulator.rosinstall
    catkin_make

Fix any compilation errors related to dependency.

To run the code, refer to https://sdk.rethinkrobotics.com/wiki/Simulator_Installation from section "Edit baxter.sh". Then follow further examples at https://sdk.rethinkrobotics.com/wiki/Hello_Baxter from section "Echo a ROS Topic".
    
Code & Tickets
--------------

+-----------------+----------------------------------------------------------------+
| Documentation   | http://sdk.rethinkrobotics.com/wiki                            |
+-----------------+----------------------------------------------------------------+
| Issues          | https://github.com/RethinkRobotics/baxter_simulator/issues     |
+-----------------+----------------------------------------------------------------+
| Contributions   | http://sdk.rethinkrobotics.com/wiki/Contributions              |
+-----------------+----------------------------------------------------------------+

baxter_simulator Repository Overview
------------------------------------

::

     .
     |
     +-- baxter_simulator/        baxter_simulator metapackage
     |
     +-- baxter_gazebo/           Gazebo interface for the Baxter that loads the models into simulation
     |   +-- src/
     |   +-- launch/
     |   +-- worlds/
     |
     +-- baxter_sim_controllers/  Controller plugins for Baxter
     |   +-- src/
     |   +-- include/
     |   +-- config/
     |
     +-- baxter_sim_examples/     Examples specific to Baxter in Simulation
     |   +-- scripts/             (use baxter_examples for examples that will work both in
     |   +-- include/              simulation AND the real Baxter robot)
     |   +-- launch/
     |   +-- models/
     |
     +-- baxter_sim_hardware/     This emulates the hardware interfaces of Baxter 
     |   +-- src/
     |   +-- include/
     |   +-- config/
     |   +-- launch/
     |
     +-- baxter_sim_io/           QT based navigator plugins for baxter
     |   +-- src/
     |   +-- include/
     |   +-- ui/
     |
     +-- baxter_sim_kinematics/     Implementation of IK, FK and gravity compensation for baxter 
     |   +-- src/
     |   +-- include/
     |   +-- launch/



Other Baxter Repositories
-------------------------

+------------------+-----------------------------------------------------+
| baxter           | https://github.com/RethinkRobotics/baxter           |
+------------------+-----------------------------------------------------+
| baxter_interface | https://github.com/RethinkRobotics/baxter_interface |
+------------------+-----------------------------------------------------+
| baxter_tools     | https://github.com/RethinkRobotics/baxter_tools     |
+------------------+-----------------------------------------------------+
| baxter_examples  | https://github.com/RethinkRobotics/baxter_examples  |
+------------------+-----------------------------------------------------+
| baxter_common    | https://github.com/RethinkRobotics/baxter_common    |
+------------------+-----------------------------------------------------+

Latest Release Information
--------------------------

http://sdk.rethinkrobotics.com/wiki/Release-Changes
