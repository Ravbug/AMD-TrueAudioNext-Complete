cmake_minimum_required(VERSION 3.17)

project(TAN-complete)

set(CMAKE_CXX_STANDARD 14)
set(CMAKE_CXX_STANDARD_REQUIRED ON)
enable_language(CXX)

set(CMAKE_C_FLAGS_DEBUG "${CMAKE_C_FLAGS_DEBUG} -D_DEBUG")
if(NOT WIN32)
if(APPLE)
#SET (CMAKE_CXX_COMPILER "/usr/bin/c++")
set(CMAKE_CXX_FLAGS_DEBUG "-Xpreprocessor -fopenmp -lomp")
set(CMAKE_CXX_FLAGS "-Xpreprocessor -fopenmp -lomp")
#set(CMAKE_SHARED_LINKER_FLAGS " -lomp" )
else()
set(CMAKE_CXX_FLAGS_DEBUG "-fopenmp")
set(CMAKE_CXX_FLAGS "-fopenmp")
endif()
endif()

#libraries
find_package ( OPENMP REQUIRED )


set(TAN_ROOT "${CMAKE_SOURCE_DIR}/TAN")
set(OpenCL_INCLUDE_DIR "${TAN_ROOT}/thirdparty/OpenCL-Headers")
set(DEFINE_AMD_OPENCL_EXTENSION ON CACHE INTERNAL "")

add_subdirectory(TAN/tan/samples/proj/cmake/CLKernelPreprocessor cmake-CLKernelPreprocessor-bin)
add_subdirectory(TAN/tan/tanlibrary/proj/cmake/amf cmake-amf-bin)
add_subdirectory(TAN/tan/tanlibrary/proj/cmake/Graal cmake-Graal-bin)
add_subdirectory(TAN/tan/tanlibrary/proj/cmake/Graal2 cmake-Graal2-bin)
add_subdirectory(TAN/tan/tanlibrary/proj/cmake/clFFT cmake-clFFT-bin)

# main
add_subdirectory(TAN/tan/tanlibrary/proj/cmake/TAN cmake-TAN-bin)