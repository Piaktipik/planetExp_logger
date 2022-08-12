cmake_minimum_required(VERSION 2.8.3)
project(planetexp_logger)

find_package(catkin REQUIRED COMPONENTS dynamic_reconfigure message_generation roscpp rosgraph_msgs rospy std_msgs)

add_message_files(
  FILES
  NodeExampleData.msg
)

generate_messages(
  DEPENDENCIES
  std_msgs
)

generate_dynamic_reconfigure_options(
  cfg/nodeExample.cfg
)

catkin_package(
  CATKIN_DEPENDS dynamic_reconfigure message_runtime roscpp rosgraph_msgs rospy std_msgs
)

include_directories(include ${catkin_INCLUDE_DIRS})

catkin_install_python(PROGRAMS src/pylistener.py src/pytalker.py DESTINATION ${CATKIN_PACKAGE_BIN_DESTINATION})

install(TARGETS listener talker
  RUNTIME DESTINATION ${CATKIN_PACKAGE_BIN_DESTINATION}
  LIBRARY DESTINATION ${CATKIN_PACKAGE_LIB_DESTINATION}
  ARCHIVE DESTINATION ${CATKIN_PACKAGE_LIB_DESTINATION}
)

install(DIRECTORY launch
  DESTINATION ${CATKIN_PACKAGE_SHARE_DESTINATION}
)