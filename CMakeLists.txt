cmake_minimum_required(VERSION 3.14)
project(cpp_protocol_sm)

set(CMAKE_CXX_STANDARD 17)

enable_testing()
include(CTest)

if (MSVC)
    # warning level 4 and all warnings as errors
    add_compile_options(/W4 /WX)
else()
    # lots of warnings and all warnings as errors
    add_compile_options(-Wall -Wextra -pedantic -Werror)
endif()

add_subdirectory(test)
add_subdirectory(src)