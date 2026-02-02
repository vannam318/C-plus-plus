cmake_minimum_required(VERSION 3.10)
project(C_C_plus_plus_project VERSION 1.0 LANGUAGES CXX)

set(CMAKE_CXX_STANDARD 17)
set(CMAKE_CXX_STANDARD_REQUIRED ON)
set(CMAKE_CXX_EXTENSIONS OFF)

# Collect root .cpp files (Compile_process handled as subdirectory)
file(GLOB ROOT_SOURCES
    ${CMAKE_SOURCE_DIR}/*.cpp
)

add_subdirectory(Compile_process)

add_executable(program ${ROOT_SOURCES})

# Ensure headers are visible
target_include_directories(program PRIVATE
    ${CMAKE_SOURCE_DIR}
)

# Link the module library built from Compile_process
target_link_libraries(program PRIVATE compile_process)

# Common compile options
if(MSVC)
    target_compile_options(program PRIVATE /W4 /permissive-)
else()
    target_compile_options(program PRIVATE -Wall -Wextra -Wpedantic)
endif()

# Install target
install(TARGETS program RUNTIME DESTINATION bin)

message(STATUS "Project sources: ${PROJECT_SOURCES}")
