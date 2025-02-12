cmake_minimum_required(VERSION 3.0.2)
project(open_scenario_helper)

## Compile as C++11, supported in ROS Kinetic and newer
# add_compile_options(-std=c++11)

## Find catkin macros and libraries
find_package(catkin REQUIRED COMPONENTS
)

catkin_package(
  INCLUDE_DIRS include
  LIBRARIES ${PROJECT_NAME}
)

###########
## Build ##
###########

include_directories(
  ${catkin_INCLUDE_DIRS}
  include
  ${CMAKE_CURRENT_SOURCE_DIR}/include/ad-xolib/build/src/xosc
  ${CMAKE_CURRENT_SOURCE_DIR}/include/ad-xolib/build/src/xoeng
  ${CMAKE_CURRENT_SOURCE_DIR}/include/ad-xolib/build/src/xodr
  ${CMAKE_CURRENT_SOURCE_DIR}/include/ad-xolib/src/xodr
  ${CMAKE_CURRENT_SOURCE_DIR}/include/ad-xolib/src/xoeng
  ${CMAKE_CURRENT_SOURCE_DIR}/include/ad-xolib/src/xosc
  ${CMAKE_CURRENT_SOURCE_DIR}/include/ad-xolib/src
  ${CMAKE_CURRENT_SOURCE_DIR}/include/pugi
  ${CMAKE_CURRENT_SOURCE_DIR}/include
)

add_library(
  ${PROJECT_NAME}
  ${CMAKE_CURRENT_SOURCE_DIR}/src/openScenarioHelper.cpp
)

find_library(XOSC_LIBRARY
NAMES xosc
HINTS "${CMAKE_CURRENT_SOURCE_DIR}/include/ad-xolib/build/src/xosc"
)
find_library(XOENG_LIBRARY
NAMES xoeng
HINTS "${CMAKE_CURRENT_SOURCE_DIR}/include/ad-xolib/build/src/xoeng"
)
find_library(XODR_LIBRARY
NAMES xodr
HINTS "${CMAKE_CURRENT_SOURCE_DIR}/include/ad-xolib/build/src/xodr"
)

target_link_libraries(${PROJECT_NAME}
  ${catkin_LIBRARIES}
  ${XOSC_LIBRARY}
  ${XOENG_LIBRARY}
  ${XODR_LIBRARY}
)


install(TARGETS ${PROJECT_NAME}
  ARCHIVE DESTINATION ${CATKIN_PACKAGE_LIB_DESTINATION}
  LIBRARY DESTINATION ${CATKIN_PACKAGE_LIB_DESTINATION}
  RUNTIME DESTINATION ${CATKIN_GLOBAL_BIN_DESTINATION}
)