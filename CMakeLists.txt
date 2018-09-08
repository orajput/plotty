cmake_minimum_required(VERSION 3.0)
project(plotty)

add_definitions(-std=c++11 -Wall -O3)

# The matplotlib-cpp headers are linked against
find_package(PythonLibs 2.7 REQUIRED)
find_package(Eigen3 REQUIRED)

find_package(PkgConfig REQUIRED)
message(STATUS "Make sure the location libglog.pc is in ENV{PKG_CONFIG_PATH}: $ENV{PKG_CONFIG_PATH}")
pkg_search_module(PKG_GLOG REQUIRED libglog)

include_directories(${PYTHON_INCLUDE_DIRS} ${EIGEN3_INCLUDE_DIRS})
include_directories(${PROJECT_SOURCE_DIR}/include)

#############
# LIBRARIES #
#############
set(HEADERS
    include/plotty/matplotlibcpp.hpp
  )

set(SOURCES
    src/matplotlibcpp.cpp
  )
add_library(${PROJECT_NAME} ${SOURCES} ${HEADERS})
target_link_libraries(${PROJECT_NAME} ${PYTHON_LIBRARY} ${PKG_GLOG_LIBRARIES})

###############
# EXECUTABLES #
###############

add_executable(mpl_example_node src/mpl_example_node.cpp)
target_link_libraries(mpl_example_node ${PROJECT_NAME})
