# 1. Find Vulkan HERE, not in root
find_package(Vulkan REQUIRED)

# 2. Find sources
file(GLOB_RECURSE ENGINE_SOURCES "src/*.c")

# 3. Define the library
add_library(engine SHARED ${ENGINE_SOURCES})

# 4. Include Directories
target_include_directories(engine PUBLIC
    ${CMAKE_CURRENT_SOURCE_DIR}/src
    ${Vulkan_INCLUDE_DIRS}
)

# 5. Engine Defines
target_compile_definitions(engine PRIVATE
    KEXPORT
)

if(WIN32)
    target_compile_definitions(engine PRIVATE
        _CRT_SECURE_NO_WARNINGS
    )
endif()

# 6. Engine Flags
# target_compile_options(engine PRIVATE -Werror)

# 7. Link libraries
target_link_libraries(engine PRIVATE
    ${Vulkan_LIBRARIES}
)

if(WIN32)
    target_link_libraries(engine PRIVATE user32)
endif()

if(UNIX AND NOT APPLE)
    target_link_libraries(engine PRIVATE
        xcb
        X11
        X11-xcb
    )
endif()
