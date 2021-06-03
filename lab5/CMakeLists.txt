cmake_minimum_required(VERSION 3.12)

project(print)

option(BUILD_TESTS "Build tests" OFF)

include_directories(lib)
add_library(print STATIC lib/print.cpp)

if(BUILD_TESTS)
  enable_testing()
  add_subdirectory(third-party/gtest)
  file(GLOB PRINT_TEST_SOURCES tests/*.cpp)
  add_executable(check ${PRINT_TEST_SOURCES})
  target_link_libraries(check print gtest_main)
  add_test(NAME check COMMAND check)
endif()
