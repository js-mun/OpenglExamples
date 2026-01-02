cmake_minimum_required(VERSION 3.10)
project(HelloTriangle)

set(CMAKE_CXX_STANDARD 17)

# OpenGL / GLFW
find_package(OpenGL REQUIRED)
find_package(glfw3 REQUIRED)

# GLAD
add_library(glad STATIC
    external/glad_1/src/glad.c
)

target_link_libraries(glad PRIVATE ${CMAKE_DL_LIBS})
target_include_directories(glad PUBLIC
    external/glad_1/include
)

# 실행 파일
add_executable(HelloTriangle
    src/main.cpp
)

target_include_directories(HelloTriangle PRIVATE include)

target_link_libraries(HelloTriangle
    glad
    glfw
    OpenGL::GL
)

configure_file(${CMAKE_CURRENT_SOURCE_DIR}/src/3.3.shader.vs ${CMAKE_CURRENT_BINARY_DIR}/3.3.shader.vs COPYONLY)
configure_file(${CMAKE_CURRENT_SOURCE_DIR}/src/3.3.shader.fs ${CMAKE_CURRENT_BINARY_DIR}/3.3.shader.fs COPYONLY)
