if(USE_FETCH_CONTENT)
    include(FetchContent)

    FetchContent_Declare(json URL https://github.com/nlohmann/json/releases/download/v3.10.4/json.tar.xz)
    FetchContent_MakeAvailable(json)
else() 
    find_package(nlohmann_json REQUIRED)
endif()

add_subdirectory(test)

set(LIB_NAME JsonHistoryParser)

aux_source_directory(. SRC_FILES)

add_library(${LIB_NAME} STATIC ${SRC_FILES})

target_link_libraries(${LIB_NAME} PUBLIC ExpressionHistoryParserInterface)
target_link_libraries(${LIB_NAME} PRIVATE nlohmann_json::nlohmann_json)

target_include_directories(${LIB_NAME} INTERFACE .)

