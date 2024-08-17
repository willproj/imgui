cmake_minimum_required(VERSION 3.22)

project(ImGui)

# List of core ImGui source files
set(IMGUI_SRC
    imgui.cpp
    imgui_demo.cpp
    imgui_draw.cpp
    imgui_tables.cpp
    imgui_widgets.cpp
)

# Backend source files for OpenGL and Vulkan
set(IMGUI_BACKENDS_SRC
    backends/imgui_impl_opengl3.cpp
    backends/imgui_impl_vulkan.cpp
)

# Add ImGui library as a static library
add_library(imgui STATIC ${IMGUI_SRC} ${IMGUI_BACKENDS_SRC})

# Include directories for ImGui and backends
target_include_directories(imgui PUBLIC
    ${CMAKE_CURRENT_SOURCE_DIR}
    ${CMAKE_CURRENT_SOURCE_DIR}/backends
)

# Link with Vulkan and OpenGL libraries
find_package(Vulkan REQUIRED)

target_link_libraries(imgui PUBLIC
    Vulkan::Vulkan
)
