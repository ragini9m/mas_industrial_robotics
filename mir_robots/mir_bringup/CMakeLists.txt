cmake_minimum_required(VERSION 2.8.3)
project(mir_bringup)

find_package(catkin REQUIRED)

catkin_package(
  CATKIN_DEPENDS
    urg_node
    mcr_collision_velocity_filter
    mcr_default_env_config
    mir_arm_cartesian_control
    mir_default_robot_config
    mir_gripper_controller
    mir_hardware_config
    mir_teleop
    openni_launch
    openni2_launch
    robot_state_publisher
    tf
    youbot_dashboard
    youbot_description
    youbot_diagnostic_aggregator
    youbot_driver_ros_interface
    usb_cam
)

### TEST
if(CATKIN_ENABLE_TESTING)
  find_package(roslaunch REQUIRED)

  #roslaunch_add_file_check(robot.launch robot:=youbot-brsu-1)
  roslaunch_add_file_check(robots)
  roslaunch_add_file_check(components robot:=youbot-brsu-1)
  roslaunch_add_file_check(tools)
endif()


### INSTALLS
set(
  INSTALL_DIRS
    components
    robots
    tools
)
foreach(dir ${INSTALL_DIRS})
  install(DIRECTORY ${dir}
    DESTINATION ${CATKIN_PACKAGE_SHARE_DESTINATION}/${dir})
endforeach()

install(FILES robot.launch
    DESTINATION ${CATKIN_PACKAGE_SHARE_DESTINATION}
  )
