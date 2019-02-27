cmake_minimum_required(VERSION 3.9)
project(fast_addr_to_data_container)

set(CMAKE_CXX_STANDARD 14)

enable_testing()
include(CTest)

add_subdirectory(test)
add_subdirectory(src)

 
