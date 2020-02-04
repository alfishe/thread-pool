# CMake entry point
cmake_minimum_required (VERSION 3.5)
project (thread-pool)

# Specify the C++ standard
set(CMAKE_CXX_STANDARD 11)
set(CMAKE_CXX_STANDARD_REQUIRED True)

# Google test
get_filename_component(GOOGLETEST_DIR lib/googletest ABSOLUTE BASE_DIR ${CMAKE_CURRENT_SOURCE_DIR})
add_subdirectory(${GOOGLETEST_DIR} ${CMAKE_CURRENT_BINARY_DIR}/googletest)

# Google benchmark
get_filename_component(GOOGLEBENCHMARK_DIR lib/benchmark ABSOLUTE BASE_DIR ${CMAKE_CURRENT_SOURCE_DIR})
add_subdirectory(${GOOGLEBENCHMARK_DIR} ${CMAKE_CURRENT_BINARY_DIR}/googlebenchmark)

# Compiler include folders
include_directories(${CMAKE_CURRENT_SOURCE_DIR}/include)
include_directories(${GOOGLETEST_DIR}/googletest/include)
include_directories(${GOOGLEBENCHMARK_DIR}/include)

# Store executable into /bin subfolder
set(CMAKE_RUNTIME_OUTPUT_DIRECTORY ${CMAKE_BINARY_DIR}/bin)

# Compile following .cpp sources
set(SOURCES ${CMAKE_CURRENT_SOURCE_DIR}/example/example.cpp)

# Compile example into executable
add_executable(${PROJECT_NAME} ${SOURCES})

# Link with following libraries
target_link_libraries(${PROJECT_NAME} pthread gtest benchmark)