project(foo)
cmake_minimum_required(VERSION 2.8)

# Configuring build type. Use "-DCMAKE_BUILD_TYPE=Release"
if(NOT CMAKE_BUILD_TYPE)
    set(CMAKE_BUILD_TYPE "Release" CACHE STRING
        "Choose the type of build, options are: Debug Release."
        FORCE)
endif(NOT CMAKE_BUILD_TYPE)
if(CMAKE_BUILD_TYPE MATCHES "Release")
    ADD_DEFINITIONS(-DQT_NO_DEBUG_OUTPUT)
endif(CMAKE_BUILD_TYPE MATCHES "Release")
message("Build type for project '${PROJECT_NAME}' set to '${CMAKE_BUILD_TYPE}'")

set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -std=c++11")

file(GLOB ProjectSources "./*.cc")

add_executable(${PROJECT_NAME}
               ${ProjectSources}
              )

install(TARGETS ${PROJECT_NAME}
        RUNTIME DESTINATION /usr/bin
        CONFIGURATIONS Release
        )
