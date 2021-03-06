configure_file(
  "${PROJECT_SOURCE_DIR}/cmake/CTestCustom.cmake"
  "${PROJECT_BINARY_DIR}/CTestCustom.cmake"
  COPYONLY)

add_executable(mio.test test.cpp)
target_link_libraries(mio.test PRIVATE mio::mio)
add_test(NAME mio.test COMMAND mio.test)

if(WIN32)
    add_executable(mio.unicode.test test.cpp)
    target_link_libraries(mio.unicode.test PRIVATE mio::mio)
    target_compile_definitions(mio.unicode.test PRIVATE UNICODE)
    add_test(NAME mio.unicode.test COMMAND mio.test)

    add_executable(mio.fullwinapi.test test.cpp)
    target_link_libraries(mio.fullwinapi.test 
      PRIVATE mio::mio_full_winapi)
    add_test(NAME mio.fullwinapi.test COMMAND mio.fullwinapi.test)

    add_executable(mio.fullwinapi.test test.cpp)
    target_link_libraries(mio.fullwinapi.test 
      PRIVATE mio::mio_min_winapi)
    add_test(NAME mio.minwinapi.test COMMAND mio.minwinapi.test)
endif()
