cmake_minimum_required(VERSION 3.10)
project(atomic_bench)

set(CMAKE_CXX_STANDARD 17)

enable_testing()
include(CTest)

add_subdirectory(test)
add_subdirectory(src)

 
