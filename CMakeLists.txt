cmake_minimum_required(VERSION 3.19)
project(OpenGLStarter)

set(CMAKE_CXX_STANDARD 14)

add_executable(${CMAKE_PROJECT_NAME} main.cpp)

find_package(OpenGL REQUIRED)

target_include_directories (${CMAKE_PROJECT_NAME}
        PRIVATE ${PROJECT_SOURCE_DIR}/ext/glew/include
        PRIVATE ${PROJECT_SOURCE_DIR}/ext/glfw/include
        PRIVATE ${PROJECT_SOURCE_DIR}/ext/glm
        PRIVATE ${PROJECT_SOURCE_DIR}/src
        )

# Set up paths so lib files and program is put together. (in this case only bin dir
# is used, add archive and library output dirs for completeness)
set_target_properties (${CMAKE_PROJECT_NAME}
        PROPERTIES
        ARCHIVE_OUTPUT_DIRECTORY "${CMAKE_BINARY_DIR}/lib"
        LIBRARY_OUTPUT_DIRECTORY "${CMAKE_BINARY_DIR}/lib"
        RUNTIME_OUTPUT_DIRECTORY "${CMAKE_BINARY_DIR}/bin"
        )

## add glew
# Note: Builds both shared and static libraries. There is sadly no option to only build one or the other
add_subdirectory(ext/glew/build/cmake)

## add glfw
add_subdirectory(ext/glfw)

target_link_libraries(${CMAKE_PROJECT_NAME}
        PRIVATE glew
        PRIVATE glfw
        )