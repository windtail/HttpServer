
set(SOURCES
    httpServer/httpConnection.cpp
    httpServer/httpData.cpp
    httpServer/httpRequest.cpp
    httpServer/httpRequestRouter.cpp
    httpServer/httpResponse.cpp
    httpServer/httpServer.cpp
    httpServer/middleware/CORS.cpp
    httpServer/middleware/auth.cpp
    httpServer/middleware/getArray.cpp
    httpServer/middleware/getObject.cpp
    httpServer/middleware/verifyJson.cpp
    httpServer/util.cpp)

set(HEADERS
    httpServer/const.h
    httpServer/httpConnection.h
    httpServer/httpCookie.h
    httpServer/httpData.h
    httpServer/httpRequest.h
    httpServer/httpRequestHandler.h
    httpServer/httpRequestRouter.h
    httpServer/httpResponse.h
    httpServer/httpServer.h
    httpServer/httpServerConfig.h
    httpServer/middleware.h
    httpServer/util.h)

add_library(httpServer ${LIBRARY_TYPE}
    ${SOURCES}
    ${HEADERS})

target_compile_definitions(httpServer PRIVATE HTTPSERVER_LIBRARY)

target_link_libraries(httpServer
    PUBLIC Qt${QT_VERSION_MAJOR}::Core
    PUBLIC Qt${QT_VERSION_MAJOR}::Network
    PUBLIC qtpromise)

include(FindZLIB)
target_link_libraries(httpServer PUBLIC ZLIB::ZLIB)

include(GNUInstallDirs)
install(TARGETS httpServer)
install(FILES ${HEADERS} DESTINATION ${CMAKE_INSTALL_INCLUDEDIR}/httpServer)
