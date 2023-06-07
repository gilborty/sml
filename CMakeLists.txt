cmake_minimum_required(VERSION 3.5)
project(boost_sml)

if(NOT CMAKE_CXX_STANDARD)
  set(CMAKE_CXX_STANDARD 17)
endif()

find_package(ament_cmake REQUIRED)

target_include_directories(boost_sml PUBLIC
    $<BUILD_INTERFACE:${CMAKE_CURRENT_SOURCE_DIR}/sml/include>
    $<INSTALL_INTERFACE:include>)

ament_export_include_directories(include)

install(FILES
  sml/include/boost/sml.hpp
  DESTINATION include/boost)

install(FILES
  sml/include/boost/sml/utility/dispatch_table.hpp
  DESTINATION include/boost/sml/utility)

ament_package()