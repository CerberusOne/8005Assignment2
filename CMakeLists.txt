cmake_minimum_required (VERSION 2.6)
project (8005-asn2)

set (8005-asn2_VERSION_MAJOR 1)
set (8005-asn2_VERSION_MINOR 0)

if(NOT CMAKE_BUILD_TYPE)
  set(CMAKE_BUILD_TYPE Release)
endif()

set(CMAKE_CXX_FLAGS "-Wall -Wextra")
set(CMAKE_CXX_FLAGS_DEBUG "-g")
set(CMAKE_CXX_FLAGS_RELEASE "-Ofast -s -fno-ident  -march=native -flto -DNDEBUG")


set(CMAKE_RUNTIME_OUTPUT_DIRECTORY ${CMAKE_BINARY_DIR}/bin)

add_definitions(-D_POSIX_C_SOURCE=200809L)
add_definitions(-D_DEFAULT_SOURCE)

include_directories(src)

file(GLOB MAIN
    "src/*.c"
    "src/*.cpp"
    )

add_executable(8005-asn2 ${MAIN})
set(THREADS_PREFER_PTHREAD_FLAG ON)
find_package(Threads REQUIRED)

find_package(OpenMP REQUIRED)
set (CMAKE_C_FLAGS "${CMAKE_C_FLAGS} ${OpenMP_C_FLAGS}")
set (CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} ${OpenMP_CXX_FLAGS}")
target_link_libraries(8005-asn2 rt Threads::Threads)
