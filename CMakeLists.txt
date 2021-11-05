cmake_minimum_required(VERSION 3.20)

project(MyProject)

set(CMAKE_MODULE_PATH "${CMAKE_CURRENT_SOURCE_DIR}/cmake/modules")

set(ABSL_PROPAGATE_CXX_STD ON)
find_package(absl REQUIRED)

add_library(MyStaticLibTarget STATIC MyStaticLib.cpp)
target_link_libraries(MyStaticLibTarget absl::strings absl::flat_hash_map)

install(TARGETS MyStaticLibTarget EXPORT MyProjectTargets)
install(TARGETS strings EXPORT MyProjectTargets)
install(TARGETS flat_hash_map EXPORT MyProjectTargets)

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

export(TARGETS
  flat_hash_map
  algorithm_container
  hash_function_defaults
  raw_hash_map
  raw_hash_set
  hash
  container_memory
  utility
  low_level_hash
  fixed_array
  optional
  variant
  algorithm
  bad_optional_access
  bad_variant_access
  hashtablez_sampler
  city
  compressed_tuple
  have_sse
  sample_recorder
  synchronization
  stacktrace
  symbolize
  time
  malloc_internal
  civil_time
  time_zone
  debugging_internal
  graphcycles_internal
  kernel_timeout_internal
  demangle_internal
  hash_policy_traits
  hashtable_debug_hooks
  exponential_biased
  cord
  container_common
  function_ref
  inlined_vector
  cordz_update_tracker
  cordz_info
  cordz_update_scope
  inlined_vector_internal
  span
  cord_internal
  cordz_functions
  cordz_handle
  cordz_statistics
  layout
  APPEND FILE lib/cmake/MyProject/MyProjectTargets.cmake)



# Setup for downstream clients of MyProject?
install(EXPORT MyProjectTargets DESTINATION lib/cmake/MyProject COMPONENT cmake-exports)
