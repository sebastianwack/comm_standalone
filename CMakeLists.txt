cmake_minimum_required(VERSION 3.4.3 FATAL_ERROR)

project(distarray)
enable_testing()

find_package(AnyDSL_runtime REQUIRED)
include_directories(${AnyDSL_runtime_INCLUDE_DIRS})

find_package(MPI)
if (MPI_FOUND)
    message("MPI MODE")
    include_directories(SYSTEM ${MPI_INCLUDE_PATH})
    set( USING_MPI TRUE)
    set( CMAKE_CXX_FLAGS "-DUSING_MPI")
else (MPI_FOUND)
    message("NO_MPI MODE")
    set( USING_MPI FALSE)
endif (MPI_FOUND)

set(CLANG_FLAGS -O3 CACHE STRING "Clang compilation options")
set(IMPALA_FLAGS -O3 --log-level info)
set(ANYDSL_RUNTIME_LIBRARIES ${AnyDSL_runtime_LIBRARIES})

set(CMAKE_CXX_STANDARD 17)
set(CXX_STANDARD_REQUIRED ON)
set(CXX_EXTENSIONS OFF)

add_subdirectory(src)
