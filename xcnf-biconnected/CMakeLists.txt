project(classify)
cmake_minimum_required( VERSION 2.4.5 )
mark_as_advanced(CMAKE_BACKWARDS_COMPATIBILITY)
set(FLAGS  "-Wall -std=c++0x")
set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} ${FLAGS}")
if(CMAKE_BUILD_TYPE MATCHES "debug")
    set(CMAKE_CXX_FLAGS "-g -ggdb ${FLAGS}")
    set(DEBUG 1)
    add_definitions("-DDEBUG -DVERIFY")
    message("Debugging symbols")
else(CMAKE_BUILD_TYPE MATCHES "debug")
#   add_definitions("-DNDEBUG")
    message("No debugging symbols")
endif(CMAKE_BUILD_TYPE MATCHES "debug")

if(CMAKE_BUILD_TYPE MATCHES "profile")
    set(CMAKE_CXX_FLAGS "${FLAGS} -g -O2")
    message("Profiling build")
endif(CMAKE_BUILD_TYPE MATCHES "profile")
add_executable(xcnf-biconnected xcnf-biconnected.cpp)
