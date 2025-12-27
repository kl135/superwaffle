cmake_minimum_required(VERSION 3.12)
project(Superwaffle)

# Force Ninja
set(CMAKE_GENERATOR "Ninja")

# Fetch raylib
include(FetchContent)
FetchContent_Declare(
  raylib
  GIT_REPOSITORY https://github.com/raysan5/raylib.git
  GIT_TAG 5.5
)
set(BUILD_EXAMPLES OFF CACHE BOOL "" FORCE) # Skip examples to speed up build
FetchContent_MakeAvailable(raylib)

# Create executable
add_executable(${PROJECT_NAME} src/main.c)

# Link raylib
target_link_libraries(${PROJECT_NAME} raylib)

# Windows specific flags for a clean windowed app
if(WIN32)
    target_link_libraries(${PROJECT_NAME} winmm gdi32)
endif()