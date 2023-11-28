cmake_minimum_required(VERSION 3.5)
project(minetest-launcher)

set(CMAKE_CXX_STANDARD 20)
set(DEP_PATH "deps")

add_executable(launcher 
    src/main.cpp
    #
    # Dear Imgui sources
    #
    ${DEP_PATH}/imgui/imgui.cpp
    ${DEP_PATH}/imgui/imgui_draw.cpp
    ${DEP_PATH}/imgui/imgui_tables.cpp
    ${DEP_PATH}/imgui/imgui_widgets.cpp
    # ${DEP_PATH}/imgui/imgui_demo.cpp
    ${DEP_PATH}/imgui/backends/imgui_impl_opengl3.cpp
    ${DEP_PATH}/imgui/backends/imgui_impl_glfw.cpp
)

set(GLFW_BUILD_DOCS OFF CACHE BOOL "" FORCE)
set(GLFW_BUILD_TESTS OFF CACHE BOOL "" FORCE)
set(GLFW_BUILD_EXAMPLES OFF CACHE BOOL "" FORCE)

add_subdirectory(${DEP_PATH}/glfw)

find_package(OpenGL REQUIRED)
target_link_libraries(launcher OpenGL::GL)

target_link_libraries(launcher glfw)

target_include_directories(launcher PRIVATE ${DEP_PATH}/imgui)
target_include_directories(launcher PRIVATE ${DEP_PATH}/imgui/backends)
target_include_directories(launcher PRIVATE ${DEP_PATH}/glfw/include)
