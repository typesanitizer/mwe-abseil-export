cmake_minimum_required(VERSION 3.20)

project(MyProject)

# This include directory needs to be the same as the argument
# to --install-folder in the README.
include("${CMAKE_BINARY_DIR}/conan/conan_paths.cmake")

set(ABSL_PROPAGATE_CXX_STD ON)
find_package(absl REQUIRED)

add_library(MyStaticLibTarget STATIC MyStaticLib.cpp)
set_property(TARGET MyStaticLibTarget PROPERTY CXX_STANDARD 11)
target_link_libraries(MyStaticLibTarget absl::strings)

install(TARGETS MyStaticLibTarget EXPORT MyProjectTargets)
# The below line (or similar absl_strings) is not needed
# because Abseil is no longer part of this build.
# install(TARGETS strings EXPORT MyProjectTargets)

if(EXPORT_MYSTATICLIB)
  # Look ma', no export error.
  export(TARGETS MyStaticLibTarget FILE lib/cmake/MyProject/MyProjectTargets.cmake)
endif()

# Setup for downstream clients of MyProject?
install(EXPORT MyProjectTargets DESTINATION lib/cmake/MyProject COMPONENT cmake-exports)
