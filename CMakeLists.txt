cmake_minimum_required(VERSION 2.8.3)
project(approxmvbb_catkin)

add_definitions(-std=c++14)

find_package(catkin_simple REQUIRED)

catkin_simple(ALL_DEPS_REQUIRED)

include(ExternalProject)

ExternalProject_Add(approxmvbb_src
  GIT_REPOSITORY  https://github.com/gabyx/ApproxMVBB.git
  GIT_TAG master
  UPDATE_COMMAND ""
  CMAKE_ARGS -DCMAKE_INSTALL_PREFIX:PATH=${CATKIN_DEVEL_PREFIX}
             -DCMAKE_BUILD_TYPE:STRING=${CMAKE_BUILD_TYPE}
)

cs_add_library(${PROJECT_NAME} src/dependency_tracker.cc)
add_dependencies(${PROJECT_NAME} approxmvbb_src)

cs_install()
cs_export()
