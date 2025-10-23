cmake_minimum_required(VERSION 3.18.1)

project(flutter_image_compress_common)

# Configure proper memory alignment for 16KB pages
set(CMAKE_C_FLAGS "${CMAKE_C_FLAGS} -DPAGE_SIZE=16384")
set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -DPAGE_SIZE=16384")

# Ensure proper alignment for memory allocations
add_definitions(-DMEMORY_ALIGNMENT=16384)

# Add platform-specific configurations
if(ANDROID)
    # Enable NEON optimizations for ARM
    if(ANDROID_ABI MATCHES "arm.*")
        set(CMAKE_C_FLAGS "${CMAKE_C_FLAGS} -mfpu=neon")
        set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -mfpu=neon")
    endif()
endif()