cmake_minimum_required(VERSION 2.8 FATAL_ERROR)

find_package(roscpp REQUIRED)
find_package(std_msgs REQUIRED)
include_directories(${roscpp_INCLUDE_DIRS})
include_directories(${std_msgs_INCLUDE_DIRS})

find_package(gazebo REQUIRED)
include_directories(${GAZEBO_INCLUDE_DIRS})
link_directories(${GAZEBO_LIBRARY_DIRS})
set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} ${GAZEBO_CXX_FLAGS}")

add_library(CameraPublisher SHARED CameraPublisher.cpp)
target_link_libraries(CameraPublisher ${GAZEBO_LIBRARIES} ${roscpp_LIBRARIES} CameraPlugin)

## Build the stand-alone test program
#add_executable(qev2_vel_pub qev2_velpub.cc)

#if (${gazebo_VERSION_MAJOR} LESS 6)
#  # These two
#  include(FindBoost)
#  find_package(Boost ${MIN_BOOST_VERSION} REQUIRED system filesystem regex)
#  target_link_libraries(qev2_vel_pub ${GAZEBO_LIBRARIES} ${Boost_LIBRARIES})
#else()
#  target_link_libraries(qev2_vel_pub ${GAZEBO_LIBRARIES})
#endif()
