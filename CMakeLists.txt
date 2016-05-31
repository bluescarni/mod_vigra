cmake_minimum_required(VERSION 3.2 FATAL_ERROR)

enable_testing()

project(vigra VERSION 0.1 LANGUAGES CXX)

set(CMAKE_MODULE_PATH ${CMAKE_MODULE_PATH} "${CMAKE_CURRENT_SOURCE_DIR}/mod_cmake")
include(ModularDeps)

set(DEP_NAME )
set(DEP_REPO )

add_dependency("array" "https://github.com/bluescarni/mod_array.git")
add_dependency("array_io" "https://github.com/bluescarni/mod_array_io.git")
add_subdirectory(deps/array)
add_subdirectory(deps/array_io)

add_library(vigra src/vigra.cpp)

target_include_directories(vigra PUBLIC
  $<BUILD_INTERFACE:${CMAKE_CURRENT_SOURCE_DIR}/include>
  $<INSTALL_INTERFACE:include>
  PRIVATE src)

install(TARGETS vigra
  ARCHIVE  DESTINATION lib
  LIBRARY  DESTINATION lib
  RUNTIME  DESTINATION bin)
install(DIRECTORY include/ DESTINATION include)

add_executable(vigra_test0 tests/vigra_test0.cpp)

target_link_libraries(vigra_test0 vigra)

add_test(vigra_test0 vigra_test0)
