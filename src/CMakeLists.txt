anydsl_runtime_wrap(MAIN_PROGRAM
    CLANG_FLAGS ${CLANG_FLAGS}
    IMPALA_FLAGS ${IMPALA_FLAGS}
    FILES comm.impala)

add_executable(main comm.cpp ${MAIN_PROGRAM})

target_link_libraries(main ${ANYDSL_RUNTIME_LIBRARIES} ${MPI_LIBRARIES})
add_test("main" main)
