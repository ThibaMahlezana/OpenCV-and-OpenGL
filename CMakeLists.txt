cmake_minimum_required(VERSION 3.20)

project(
    Video_capture
    VERSION 1.0.0
    LANGUAGES C CXX
)

set(CXX_STANDARD_REQUIRED 17)
set(SOURCES main.cpp)

# adding OpenCV library
find_package(OpenCV REQUIRED)
include_directories(${OpenCV_INCLUDE_DIRS})

# adding glfw library
set(GLFW_BUILD_DOCS OFF CACHE BOOL  "GLFW lib only")
set(GLFW_INSTALL OFF CACHE BOOL  "GLFW lib only")
add_subdirectory(glfw)
include_directories(${CMAKE_SOURCE_DIR}/glfw/include/)

# adding OpenGL Library
find_package(OpenGL REQUIRED)
include_directories(${OPENGL_INCLUDE_DIRS})

# adding glew library
include_directories(${CMAKE_SOURCE_DIR}/glew/include/)
find_library(GLEWLIB libglew32 ${CMAKE_SOURCE_DIR}/glew/lib/)

# adding ImGui Library
add_subdirectory(imgui)
include_directories(${CMAKE_SOURCE_DIR}/imgui)

# Building main target
add_executable(${PROJECT_NAME} ${SOURCES})


# linking all the libraries with the main target
target_link_libraries(
    ${PROJECT_NAME} 
    ${OpenCV_LIBS} 
    ${OPENGL_LIBRARIES}
    ${GLEWLIB}
    glfw
    imgui
)