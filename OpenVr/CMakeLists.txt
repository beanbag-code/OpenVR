set(CMAKE_OSX_ARCHITECTURES "arm64" CACHE STRING "Build for Apple Silicon" FORCE)
cmake_minimum_required(VERSION 3.10)
project(VRTrack)

# 1. Force CMake to look in the M3 Homebrew folder
list(APPEND CMAKE_PREFIX_PATH "/opt/homebrew")

# 2. Find the package
find_package(OpenCV REQUIRED)

# 1. Search paths
include_directories(/opt/homebrew/include)
include_directories(/usr/local/include)
link_directories(/opt/homebrew/lib)
link_directories(/usr/local/lib)

# 2. ImGui source files
file(GLOB IMGUI_SOURCES CONFIGURE_DEPENDS "${CMAKE_CURRENT_SOURCE_DIR}/external/ImGui/*.cpp")
include_directories(${CMAKE_CURRENT_SOURCE_DIR}/external/ImGui)

# 3. The executable
add_executable(VRTrack main.cpp ${IMGUI_SOURCES})

# 4. The Linking (Explicit paths to be safe)
target_link_libraries(VRTrack PRIVATE 
    ${OpenCV_LIBS}
    "/usr/local/lib/libapriltag.dylib"
    "/opt/homebrew/lib/libglfw.dylib"
    "/opt/homebrew/lib/libglew.dylib"
    "-framework OpenGL"
    "-framework Cocoa"
    "-framework IOKit"
    "-framework CoreVideo"
)