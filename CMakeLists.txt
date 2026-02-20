cmake_minimum_required(VERSION 3.10.0)
project(simulate_electronics VERSION 0.1.0 LANGUAGES C CXX)

file(GLOB SRC "src/*.cpp")
file(GLOB INCL "include/*.h")

include(FetchContent)

FetchContent_Declare(
    glad
    GIT_REPOSITORY https://github.com/Dav1dde/glad.git
    GIT_TAG v2.0.8
    GIT_PROGRESS   TRUE
    SOURCE_SUBDIR  cmake
)
FetchContent_MakeAvailable(glad)
glad_add_library(
    glad_gl_core_46
    STATIC
    REPRODUCIBLE
    LOADER
    API gl:core=4.6
)

set(GLFW_BUILD_DOCS OFF CACHE BOOL "" FORCE)
set(GLFW_BUILD_EXAMPLES OFF CACHE BOOL "" FORCE)
set(GLFW_BUILD_TESTS OFF CACHE BOOL "" FORCE)
set(GLFW_INSTALL OFF CACHE BOOL "" FORCE)
FetchContent_Declare(
    glfw
    GIT_REPOSITORY https://github.com/glfw/glfw.git
    GIT_TAG 3.4
)
FetchContent_MakeAvailable(glfw)

FetchContent_Declare(
        spdlog
        GIT_REPOSITORY https://github.com/gabime/spdlog.git
        GIT_TAG        v1.17.0
)
FetchContent_MakeAvailable(spdlog)

add_executable(simulate_electronics ${SRC})

target_link_libraries(simulate_electronics
    glfw
    glad_gl_core_46
    spdlog::spdlog
)

target_include_directories(simulate_electronics PRIVATE
    ${INCL}
)
