cmake_minimum_required(VERSION 3.20)

project(MyProject)

set(CMAKE_MODULE_PATH "${CMAKE_CURRENT_SOURCE_DIR}/cmake/modules")

set(ABSL_PROPAGATE_CXX_STD ON)
find_package(absl REQUIRED)

add_library(MyStaticLibTarget STATIC MyStaticLib.cpp)
target_link_libraries(MyStaticLibTarget absl::strings)

install(TARGETS MyStaticLibTarget EXPORT MyProjectTargets)
install(TARGETS strings EXPORT MyProjectTargets)

if(EXPORT_MYSTATICLIB)
  # CMake Error in CMakeLists.txt:
  # export called with target "MyStaticLibTarget" which requires target
  #   "strings" that is not in any export set.
  export(TARGETS MyStaticLibTarget FILE lib/cmake/MyProject/MyProjectTargets.cmake)
endif()

export(TARGETS
  strings
  strings_internal
  type_traits
  base
  config
  throw_delegate
  dynamic_annotations
  log_severity
  base_internal
  raw_logging_internal
  atomic_hook
  core_headers
  spinlock_wait
  endian
  bits
  int128
  memory
  errno_saver
  meta
  APPEND FILE lib/cmake/MyProject/MyProjectTargets.cmake)

# Setup for downstream clients of MyProject?
install(EXPORT MyProjectTargets DESTINATION lib/cmake/MyProject COMPONENT cmake-exports)
