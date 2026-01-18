cmake_minimum_required(VERSION 3.16)
project(MyProject C)

# --- Global Configs ---
set(CMAKE_EXPORT_COMPILE_COMMANDS ON)
set(CMAKE_C_STANDARD 17)
set(CMAKE_C_STANDARD_REQUIRED ON)

# Output directories
set(CMAKE_RUNTIME_OUTPUT_DIRECTORY ${CMAKE_BINARY_DIR})

# Global Flags
add_compile_options(-g -Wall -Wvarargs)
add_compile_definitions(_DEBUG UNICODE _UNICODE)

# --- Add Subdirectories ---
add_subdirectory(engine)

# --- Target: Testbed ---
file(GLOB_RECURSE TESTBED_SOURCES "testbed/src/*.c")
add_executable(testbed ${TESTBED_SOURCES})
target_include_directories(testbed PRIVATE ${CMAKE_SOURCE_DIR}/testbed/src)
target_link_libraries(testbed PRIVATE engine)
