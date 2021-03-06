project(libxorsat)
cmake_minimum_required( VERSION 2.4.5 )
mark_as_advanced(CMAKE_BACKWARDS_COMPATIBILITY)
set(CMAKE_ALLOW_LOOSE_LOOP_CONSTRUCTS TRUE)
if(COMMAND cmake_policy)
    cmake_policy(SET CMP0003 NEW)
    cmake_policy(SET CMP0005 NEW)
endif(COMMAND cmake_policy)

include(CTest)
set(CMAKE_BUILD_TYPE_SHARED_LIBS ON)
#set(FLAGS  "-Wall -Werror")

if(CMAKE_BUILD_TYPE MATCHES "debug")
    set(CMAKE_CXX_FLAGS "-g -ggdb ${FLAGS}")
    set(DEBUG 1)
    add_definitions("-DDEBUG -DVERIFY -DCHECK")
    message("Debugging symbols")
else(CMAKE_BUILD_TYPE MATCHES "debug")
    add_definitions("-DNDEBUG")
    message("No debugging symbols")
endif(CMAKE_BUILD_TYPE MATCHES "debug")

if(CMAKE_BUILD_TYPE MATCHES "profile")
    set(CMAKE_CXX_FLAGS "${FLAGS} -g -O2")
#    add_definitions("-DVERIFY -DCHECK")

    message("Profiling build")
endif(CMAKE_BUILD_TYPE MATCHES "profile")

if(EXPLAIN_PQUEUE)
    add_definitions("-DEXPLAIN_PQUEUE")
endif(EXPLAIN_PQUEUE)
set(CMAKE_CXX_FLAGS_RELEASE "-O3 -fomit-frame-pointer ${FLAGS}")

include_directories(libxorsat/include libxorsat/src)
include_directories(bin-xor-module)
file(GLOB binxorsrc bin-xor-module/*.cpp bin-xor-module/*.cc)
add_library(binxor ${binxorsrc})    

file(GLOB libsrc libxorsat/src/*.cpp)
set(INST_DIR ${CMAKE_SOURCE_DIR}/dist)
set(INSTALL_OPTS LIBRARY DESTINATION ${INST_DIR}
                 RUNTIME DESTINATION ${INST_DIR})        

add_library(xorsat ${libsrc})
add_subdirectory(minisat)    

