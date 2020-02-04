# CMake entry point
cmake_minimum_required (VERSION 3.5)
project (thread-pool)

# Specify the C++ standard
set(CMAKE_CXX_STANDARD 11)
set(CMAKE_CXX_STANDARD_REQUIRED True)

include_directories(${CMAKE_CURRENT_SOURCE_DIR}/include)
 
set(SOURCES ${CMAKE_CURRENT_SOURCE_DIR}/example/example.cpp)

set(CMAKE_CXX_FLAGS -pthread)
  
# Compile example executable
add_executable(${PROJECT_NAME} ${SOURCES})

target_link_libraries(${PROJECT_NAME} pthread)