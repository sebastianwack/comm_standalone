cmake_minimum_required(VERSION 3.4.3 FATAL_ERROR)

project(comm-standalone)
enable_testing()

find_package(AnyDSL_runtime REQUIRED)
include_directories(${AnyDSL_runtime_INCLUDE_DIRS})

find_package(MPI)
if (MPI_FOUND)
    include_directories(SYSTEM ${MPI_INCLUDE_PATH})
    add_definitions( -DUSING_MPI=TRUE )
else (MPI_FOUND)
    message("Warning: MPI not found!")
endif (MPI_FOUND)

set(CLANG_FLAGS -O3 CACHE STRING "Clang compilation options")
set(IMPALA_FLAGS --log-level info)
set(ANYDSL_RUNTIME_LIBRARIES ${AnyDSL_runtime_LIBRARIES})

set(CMAKE_CXX_STANDARD 14)
set(CXX_STANDARD_REQUIRED ON)
set(CXX_EXTENSIONS OFF)

add_subdirectory(src)
