cmake_minimum_required(VERSION 3.20)
# Avoid warnings from FetchContent about timestamps
if (CMAKE_VERSION VERSION_GREATER_EQUAL "3.24.0")
  cmake_policy(SET CMP0135 NEW)
endif()

project(libome
  VERSION 1.1.0
  DESCRIPTION "Implementation of massive operator matrix elements (OMEs) of the QCD twist-2 operators in x-space"
)
set(CMAKE_CXX_STANDARD 17)

# Select "Release" build by default to enable optimisation
if(NOT CMAKE_BUILD_TYPE)
  set(CMAKE_BUILD_TYPE "Release" CACHE STRING "Set the build type (Debug, Release, MinSizeRel, RelWithDebInfo)" FORCE)
endif()

# External dependencies
find_package(GSL REQUIRED)

# Floating point exceptions (FPEs)
# Note: enabling this changes nothing in the code, but if you want to rely on
# FPEs in your code, we have to make sure that the compiler does not make
# optimisations that would raise FPEs that the original code would not have
# raised. So far, this has turned out to be an issue with clang when compiling
# for Apple arm64 CPUs. See
# https://clang.llvm.org/docs/UsersManual.html#controlling-floating-point-behavior
option(ENABLE_FPES "Enable floating point exceptions")
if(ENABLE_FPES)
  add_compile_options("$<$<COMPILE_LANG_AND_ID:CXX,Clang>:-ffp-exception-behavior=maytrap>")
  add_compile_options("$<$<COMPILE_LANG_AND_ID:CXX,AppleClang>:-ffp-exception-behavior=maytrap>")
endif()


# Main code tree
add_subdirectory(src)

include(GNUInstallDirs)
install(TARGETS ome
  EXPORT candiaTargets
  FILE_SET ome_headers DESTINATION ${CMAKE_INSTALL_INCLUDEDIR})
