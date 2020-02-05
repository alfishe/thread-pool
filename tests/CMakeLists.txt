# CMake entry point
cmake_minimum_required (VERSION 3.5)
project (tp-tests)

# Specify the C++ standard
set(CMAKE_CXX_STANDARD 11)
set(CMAKE_CXX_STANDARD_REQUIRED True)

# Library root
get_filename_component(TP_DIR ../ ABSOLUTE BASE_DIR ${CMAKE_CURRENT_SOURCE_DIR})

# Include CMake helper functions file
include(${TP_DIR}/cmake/func.cmake)

# Google test
get_filename_component(GOOGLETEST_DIR ${TP_DIR}/lib/googletest ABSOLUTE BASE_DIR ${CMAKE_CURRENT_SOURCE_DIR})
add_subdirectory(${GOOGLETEST_DIR} ${CMAKE_CURRENT_BINARY_DIR}/googletest)

# Compiler include folders
include_directories(${TP_DIR}/include)
include_directories(${GOOGLETEST_DIR}/googletest/include)

# All sources in /tests and subfolders will be compiled
file (GLOB_RECURSE SOURCES ${CMAKE_CURRENT_SOURCE_DIR}/*.cpp)
EXCLUDE_FILES_FROM_DIR_IN_LIST("${SOURCES}" "/build/" FALSE OUTVAR SOURCES) # Exclude /tests/build folder


# Compile example into executable
add_executable(${PROJECT_NAME} ${SOURCES})

# Link with following libraries
target_link_libraries(${PROJECT_NAME} pthread gtest)