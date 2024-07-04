#set minimum version (fetch_content available since 3.11)
cmake_minimum_required(VERSION 3.11)
#set project name
project(viergewinnt VERSION 0.0.1 LANGUAGES CXX)

#set variable executable
set(executable "viergewinnt")

# Specify C++ standard
set(CMAKE_CXX_STANDARD 17)
set(CMAKE_CXX_STANDARD_REQUIRED True)

# Detect the operating system
if(UNIX)
    message(STATUS "Compiling on Linux")
    add_definitions(-DOS_LINUX)
elseif(WIN32)
    message(STATUS "Compiling on Linux")
    add_definitions(-DOS_WINDOWS)
elseif(APPLE)
    message(STATUS "Compiling on macOS")
    add_definitions(-DOS_MAC)
endif()

set(Sources
    src/main.cpp
)

set(LibSources
    src/test.cpp
)

# defines a static library and adds the include folder
add_library(GameLib STATIC ${LibSources})

# set the linker language for the library to c++
set_target_properties(GameLib PROPERTIES LINKER_LANGUAGE CXX)

# adds the source files to the executable
add_executable(${executable} ${Sources})

# set the linker language for the executable
set_target_properties(${executable} PROPERTIES LINKER_LANGUAGE CXX)

# sets the include directory relativ to the project directory
target_include_directories(GameLib PUBLIC "${CMAKE_SOURCE_DIR}/inc/")
target_include_directories(${executable} PUBLIC "${CMAKE_SOURCE_DIR}/inc/")

# links the library "GameLib" with the executable
target_link_libraries(${executable} PRIVATE GameLib)

# links the opencv library with executable
target_link_libraries(${executable} PRIVATE ${OpenCV_LIBS})
