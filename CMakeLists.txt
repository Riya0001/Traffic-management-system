cmake_minimum_required(VERSION 2.8)
project(prjece650)

if (EXISTS "${CMAKE_SOURCE_DIR}/minisat")
  add_subdirectory(minisat)
else()
  message (FATAL_ERROR "MiniSat not found. Use `git clone https://git.uwaterloo.ca/ece650-1231/minisat.git` to check it out.")
endif()


## ECE650 Specific configuration start here
## Project specific configurations go here

# enable c++11 support
set (CMAKE_CXX_FLAGS "-std=c++11 -Wall ${CMAKE_CXX_FLAGS}")

# expose minisat header files
include_directories(${CMAKE_SOURCE_DIR}/minisat)

add_executable(prjece650 Graphs.cpp Parser.cpp prjece650.cpp)

target_link_libraries(prjece650 minisat-lib-static pthread)

# create the executable for tests
add_executable(test test.cpp)

# link MiniSAT libraries
target_link_libraries(test minisat-lib-static)


