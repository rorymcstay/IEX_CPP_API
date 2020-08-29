#define IEX_ENDPOINT "https://sandbox.iexapis.com/1.0"

set(LIB_SOURCES 
    IEX.cpp
)


add_library(iex_api SHARED ${LIB_SOURCES})


find_package(CURL)

if (CURL_FOUND)
    message("   found package CURL")
    message("   CURL_LIBRARIES: ${CURL_LIBRARIES}")
else()
    message("couldn't find package CURL")
endif()


target_link_libraries(iex_api PUBLIC 
    utils
    ${JSONCPP_LIBRARIES}
    ${CURL_LIBRARIES}
)

target_include_directories(iex_api PUBLIC 
    ${CMAKE_CURRENT_SOURCE_DIR}
    ${CURL_LIBRARIES}
    ${JSONCPP_INCLUDE_DIRS}
)

install(TARGETS iex_api
        RUNTIME DESTINATION bin
        LIBRARY DESTINATION lib
        ARCHIVE DESTINATION lib/static)
