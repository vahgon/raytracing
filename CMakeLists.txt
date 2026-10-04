cmake_minimum_required(VERSION 3.30)

project(
        raytacing
        VERSION 0.1
        DESCRIPTION "raytracing in one weekend"
        LANGUAGES CXX
)

set(CMAKE_CXX_STANDARD 26)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

set(CMAKE_RUNTIME_OUTPUT_DIRECTORY ${CMAKE_SOURCE_DIR}/bin)

add_executable(raytracing ${CMAKE_SOURCE_DIR}/src/main.cpp)

target_include_directories(raytracing
        PRIVATE ${CMAKE_SOURCE_DIR}/src
        PUBLIC ${CMAKE_SOURCE_DIR}/include
)

target_compile_features(raytracing PRIVATE cxx_std_26)

target_compile_options(raytracing PRIVATE
        -Wall -Wextra -Wpedantic -freflection
        $<$<CONFIG:DEBUG>:-Wconversion -Wsign-conversion -Wnrvo -g -O0>
        $<$<CONFIG:RELEASE>:-O3>
)

target_link_options(raytracing PRIVATE
        $<$<CONFIG:DEBUG>:-fsanitize=address,undefined,leak>
)