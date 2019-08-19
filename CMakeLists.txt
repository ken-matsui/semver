cmake_minimum_required(VERSION 3.0)
project(interval VERSION 0.2.1 LANGUAGES CXX)

add_executable(interval tests/interval.cpp)
target_compile_features(interval PRIVATE cxx_std_17)
target_include_directories(interval PRIVATE ${CMAKE_CURRENT_SOURCE_DIR}/include)


set(Boost_DEBUG on)
set(Boost_NO_BOOST_CMAKE ON)
find_package(Boost REQUIRED COMPONENTS unit_test_framework)
if (NOT ${Boost_FOUND})
    message(FATAL_ERROR "Could not find boost.")
endif ()
target_include_directories(interval PRIVATE ${Boost_INCLUDE_DIRS})
message(STATUS "Boost include directory is ... ${Boost_INCLUDE_DIRS}")
target_link_directories(${PROJECT_NAME} PRIVATE ${Boost_LIBRARY_DIRS})
message(STATUS "Boost library directories are ... ${Boost_LIBRARY_DIRS}")

target_link_libraries(
        interval ${Boost_UNIT_TEST_FRAMEWORK_LIBRARY}
)
install(TARGETS ${PROJECT_NAME} DESTINATION bin)

