cmake_minimum_required(VERSION 3.17)

project(TrueAudio-NEXT-complete)

set(CMAKE_CXX_STANDARD 14)
set(CMAKE_CXX_STANDARD_REQUIRED ON)
enable_language(CXX)

#libraries

if(MSVC)
  add_definitions(/MP)
  add_definitions(/Qpar)
endif()

set(TAN_ROOT "${CMAKE_SOURCE_DIR}/TAN")
set(OpenCL_INCLUDE_DIR "${TAN_ROOT}/thirdparty/OpenCL-Headers")
set(DEFINE_AMD_OPENCL_EXTENSION ON CACHE INTERNAL "")

# bundled fftw
add_subdirectory(fftw)

# bundled OpenMP
set(OPENMP_STANDALONE_BUILD ON CACHE INTERNAL "")
add_subdirectory(openmp)

# TAN components
add_subdirectory(TAN/tan/samples/proj/cmake/GPUUtilities cmake-GPUUtilities-bin)
add_subdirectory(TAN/tan/samples/proj/cmake/CLKernelPreprocessor cmake-CLKernelPreprocessor-bin)
add_subdirectory(TAN/tan/tanlibrary/proj/cmake/amf cmake-amf-bin)
add_subdirectory(TAN/tan/tanlibrary/proj/cmake/Graal cmake-Graal-bin)
add_subdirectory(TAN/tan/tanlibrary/proj/cmake/Graal2 cmake-Graal2-bin)
add_subdirectory(TAN/tan/tanlibrary/proj/cmake/clFFT cmake-clFFT-bin)
add_subdirectory(TAN/tan/samples/proj/cmake/FileToHeader cmake-FileToHeader-bin)
add_subdirectory(TAN/tan/samples/proj/cmake/TrueAudioVR cmake-TrueAudioVR-bin)
add_subdirectory(TAN/tan/tanlibrary/proj/cmake/TAN cmake-TAN-bin)

# fixup include paths
target_include_directories(Graal2 PUBLIC "${CMAKE_BINARY_DIR}/openmp/runtime/src")
target_link_libraries(TrueAudioNext fftw3 omp)
target_link_libraries(Graal2 omp)
