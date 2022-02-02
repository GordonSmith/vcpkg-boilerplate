cmake_minimum_required(VERSION 3.14)

if(CMAKE_SOURCE_DIR STREQUAL CMAKE_BINARY_DIR)
    message(FATAL_ERROR "Do not build in-source. Please remove CMakeCache.txt and the CMakeFiles/ directory. Then build out-of-source.")
endif()

project(
    "BoilerPlate"
    VERSION 0.1.0 
    LANGUAGES C CXX 
)

include(CTest)                          # Must be called before adding tests but after calling project(). This automatically calls enable_testing() and configures ctest targets when using Make/Ninja
include(CMakeDependentOption)           # This is a really useful scripts that creates options that depends on other options. It can even be used with generator expressions !
include(GNUInstallDirs)                 # This will define the default values for installation directories (all platforms even if named GNU)
include(InstallRequiredSystemLibraries) # Tell CMake that the `install` target needs to install required system libraries (eg: Windows SDK)
include(CMakePackageConfigHelpers)      # Helper to create relocatable packages

list(APPEND CMAKE_MODULE_PATH "${CMAKE_CURRENT_LIST_DIR}/cmake") # Make our cmake scripts available

set_property(GLOBAL PROPERTY USE_FOLDERS ON)

set(CMAKE_CXX_VISIBILITY_PRESET hidden)
set(CMAKE_VISIBILITY_INLINES_HIDDEN 1)

find_package(ICU REQUIRED COMPONENTS data i18n io le lx test tu uc)
find_package(ZLIB REQUIRED)
find_package(OpenSSL REQUIRED)
find_package(LibXslt REQUIRED)
find_package(FLEX REQUIRED)
find_package(BISON REQUIRED)

add_executable(BoilerPlate source/main.cpp)

# ./vcpkg.exe install --keep-going icu zlib openssl libxslt winflexbison --triplet x64-windows
