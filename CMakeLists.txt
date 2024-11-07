cmake_minimum_required(VERSION 3.10)
project(MyProject C)

# Set the C standard
set(CMAKE_C_STANDARD 99)
set(CMAKE_C_STANDARD_REQUIRED True)

# Enable compilation commands export (useful for IDEs)
set(CMAKE_EXPORT_COMPILE_COMMANDS ON)

# GLFW Build Flags
set(GLFW_BUILD_EXAMPLES OFF CACHE BOOL "" FORCE)
set(GLFW_BUILD_TESTS OFF CACHE BOOL "" FORCE)
set(GLFW_BUILD_DOCS OFF CACHE BOOL "" FORCE)

# Include directories
include_directories(
    ${CMAKE_SOURCE_DIR}/include
    external/glad/include
)

# Gather all source files in the src directory
file(GLOB SOURCES ${CMAKE_SOURCE_DIR}/src/*.c)

# Add glad library (glad source file only, headers are already in include path)
add_library(glad external/glad/src/gl.c)

# Add the main project executable
add_executable(MyProject ${SOURCES})

# Link libraries
target_link_libraries(MyProject PRIVATE
    glad
    glfw
    cglm
)

# Add subdirectories for external dependencies
add_subdirectory(external/glfw)
add_subdirectory(external/cglm)

