include(FetchContent)
FetchContent_Declare(
  googletest
  GIT_REPOSITORY https://github.com/google/googletest.git
  GIT_TAG release-1.12.1
)
# For Windows: Prevent overriding the parent project's compiler/linker settings
set(gtest_force_shared_crt ON CACHE BOOL "" FORCE)

FetchContent_Declare(
  googlebench
  GIT_REPOSITORY https://github.com/google/benchmark.git
  GIT_TAG v1.7.0
)

FetchContent_MakeAvailable(
  googletest
  googlebench
)

include(GoogleTest)

macro(add_gtest_test test_name sources)
    add_executable(${test_name} ${sources})
    target_link_libraries(${test_name} GTest::gtest_main)
    gtest_discover_tests(${test_name})
endmacro(add_gtest_test)

macro(add_gbench_bench bench_name sources)
    add_executable(${bench_name} ${sources})
    target_link_libraries(${bench_name} benchmark::benchmark_main ${ARGN})
endmacro(add_gbench_bench)

###############################################################################
add_gtest_test(minimal_test minimal_test.cpp)
add_gbench_bench(minimal_bench minimal_bench.cpp)
