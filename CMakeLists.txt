cmake_minimum_required(VERSION 3.20)
project(azmq)

option(AZMQ_NO_TESTS "Disable Tests" OFF)

find_package(Boost 1.48 COMPONENTS system date_time thread chrono random REQUIRED)
find_package(ZeroMQ 4.0 REQUIRED)

add_library(azmq INTERFACE)
target_compile_features(azmq INTERFACE cxx_std_11)
target_include_directories(azmq INTERFACE
        $<BUILD_INTERFACE:${CMAKE_CURRENT_SOURCE_DIR}>)
target_link_libraries(azmq INTERFACE
        Boost::system Boost::date_time Boost::thread Boost::chrono Boost::random
        ZeroMQ::ZeroMQ)

if(NOT AZMQ_NO_TESTS)
    enable_testing()
endif()

if(NOT AZMQ_NO_TESTS)
    add_subdirectory(test)
    add_subdirectory(doc)
endif()
