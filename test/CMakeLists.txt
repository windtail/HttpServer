
set(SOURCES main.cpp requestHandler.cpp)

set(HEADERS requestHandler.h)

add_executable(httpServerTest ${SOURCES} ${HEADERS})

target_include_directories(httpServerTest PRIVATE ${CMAKE_SOURCE_DIR}/src)
target_link_libraries(httpServerTest PRIVATE httpServer)

