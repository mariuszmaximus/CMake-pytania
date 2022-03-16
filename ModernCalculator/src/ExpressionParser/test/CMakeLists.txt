set(TEST_NAME ExpressionParserTests)

if(USE_FETCH_CONTENT)
  Include(FetchContent)

  FetchContent_Declare(
    Catch2
    GIT_REPOSITORY https://github.com/catchorg/Catch2.git
    GIT_TAG        v2.13.7)

  FetchContent_MakeAvailable(Catch2)
else()
  find_package(Catch2 REQUIRED)
endif()  


aux_source_directory(. TEST_FILES)

add_executable(${TEST_NAME} ${TEST_FILES})

target_link_libraries(${TEST_NAME} PRIVATE Catch2::Catch2)
target_link_libraries(${TEST_NAME} PRIVATE ExpressionParser)

add_test(NAME ${TEST_NAME}
        COMMAND ${TEST_NAME})