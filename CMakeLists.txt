cmake_minimum_required(VERSION 3.10)
project(WizardEngine)

# Set C++ standard
set(CMAKE_CXX_STANDARD 17)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

# Use absolute paths to avoid issues with out-of-source builds
set(PROJECT_ROOT ${CMAKE_SOURCE_DIR})
set(LIBRARIES_DIR ${PROJECT_ROOT}/Libraries)
set(SRC_DIR ${PROJECT_ROOT}/src)

# Add executable
file(GLOB SRC_FILES "${SRC_DIR}/*.cpp")
add_executable(WizardEngine ${SRC_FILES} "${LIBRARIES_DIR}/src/glad.c"  
		"Include/config.h" 
		"src/triangle_mesh.h"
		"src/triangle_mesh.cpp"
)

# Include directories
target_include_directories(WizardEngine PRIVATE "${LIBRARIES_DIR}/include")

# Link GLFW using an absolute path
target_link_libraries(WizardEngine PRIVATE "${LIBRARIES_DIR}/lib/glfw3.lib")

# Link OpenGL
find_package(OpenGL REQUIRED)
target_link_libraries(WizardEngine PRIVATE OpenGL::GL)


file(COPY ${CMAKE_SOURCE_DIR}/Shaders DESTINATION ${CMAKE_BINARY_DIR})
