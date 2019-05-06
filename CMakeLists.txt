cmake_minimum_required(VERSION 3.9)
project(cv2viewer)
set(CMAKE_CXX_STANDARD 14)

# Main
add_executable(cv2viewer
    cv2viewer.cpp
    imgui/imgui.cpp
    imgui/imgui_draw.cpp
    imgui/imgui_widgets.cpp
    imgui/examples/imgui_impl_sdl.cpp
    imgui/examples/imgui_impl_opengl3.cpp
    imgui/examples/libs/gl3w/GL/gl3w.c
)

# include: OpenCV
find_package(OpenCV REQUIRED)
if(OpenCV_FOUND)
    target_include_directories(cv2viewer PUBLIC ${OpenCV_INCLUDE_DIRS})
    target_link_libraries(cv2viewer ${OpenCV_LIBS})
endif()

# include: SDL
find_package(SDL2 REQUIRED)
include_directories(${SDL2_INCLUDE_DIRS})

# include: ImGui(symbolic linked)
include_directories(
    imgui/
    imgui/examples
    imgui/examples/libs/gl3w
)

# link
target_link_libraries(cv2viewer
    ${SDL2_LIBRARIES}
    "-framework OpenGL"
    "-framework Cocoa"
    "-framework IOKit"
    "-framework CoreVideo"
)
