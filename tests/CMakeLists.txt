find_package(GTest REQUIRED)
include(GoogleTest)

aux_source_directory(testcases UINT256_TEST_SOURCES)

add_executable(tests ${UINT256_TEST_SOURCES})
add_dependencies(tests ${UINT256_LIBRARY})

target_include_directories(tests PRIVATE ${CMAKE_CURRENT_SOURCE_DIR}/../include)
target_link_directories(tests PRIVATE ${PROJECT_BINARY_DIR})
target_link_libraries(tests PRIVATE ${UINT256_LIBRARY} GTest::GTest GTest::Main)
gtest_discover_tests(tests)
