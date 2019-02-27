# Download and unpack googletest at configure time
configure_file(${PROJECT_SOURCE_DIR}/cmake/CMakeLists_gtest.txt.in ${CMAKE_BINARY_DIR}/googletest-download/CMakeLists.txt)
execute_process(COMMAND ${CMAKE_COMMAND} -G "${CMAKE_GENERATOR}" .
  RESULT_VARIABLE result
  WORKING_DIRECTORY ${CMAKE_BINARY_DIR}/googletest-download )
if(result)
  message(FATAL_ERROR "CMake step for googletest failed: ${result}")
endif()
execute_process(COMMAND ${CMAKE_COMMAND} --build .
  RESULT_VARIABLE result
  WORKING_DIRECTORY ${CMAKE_BINARY_DIR}/googletest-download )
if(result)
  message(FATAL_ERROR "Build step for googletest failed: ${result}")
endif()

# Prevent overriding the parent project's compiler/linker
# settings on Windows
set(gtest_force_shared_crt ON CACHE BOOL "" FORCE)

# Add googletest directly to our build. This defines
# the gtest and gtest_main targets.
add_subdirectory(${CMAKE_BINARY_DIR}/googletest-src
                 ${CMAKE_BINARY_DIR}/googletest-build
                 EXCLUDE_FROM_ALL)




# Download and unpack googlebench at configure time
configure_file(${PROJECT_SOURCE_DIR}/cmake/CMakeLists_bench.txt.in ${CMAKE_BINARY_DIR}/googlebench-download/CMakeLists.txt)
set(BENCHMARK_ENABLE_TESTING OFF)
execute_process(COMMAND ${CMAKE_COMMAND} -G "${CMAKE_GENERATOR}" .
  RESULT_VARIABLE result
  WORKING_DIRECTORY ${CMAKE_BINARY_DIR}/googlebench-download )
if(result)
  message(FATAL_ERROR "CMake step for googlebench failed: ${result}")
endif()
execute_process(COMMAND ${CMAKE_COMMAND} --build .
  RESULT_VARIABLE result
  WORKING_DIRECTORY ${CMAKE_BINARY_DIR}/googlebench-download )
if(result)
  message(FATAL_ERROR "Build step for googlebench failed: ${result}")
endif()

# Add googletest directly to our build. This defines
# the gtest and gtest_main targets.
add_subdirectory(${CMAKE_BINARY_DIR}/googlebench-src
                 ${CMAKE_BINARY_DIR}/googlebench-build
                 EXCLUDE_FROM_ALL)

find_package(GTest)

# Add Benchmark ##################################################################
# add_executable(target source)
# target_link_libraries(target benchmark_main other_dep)
# add_test(NAME target COMMAND target)

# Add Test #######################################################################
# add_executable(target source)
# target_link_libraries(tagrget gtest_main other_dep)
# gtest_discover_tests(target)
