cmake_minimum_required(VERSION 3.18)

project(HttpServer)

set(CMAKE_CXX_STANDARD 11)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

option(BUILD_TESTING "build tests?" OFF)
option(BUILD_STATIC "build static library?" OFF)

set(QT_PROMISE_URL https://github.com/simonbrunel/qtpromise.git CACHE STRING "qtpromise url")
set(QT_PROMISE_TAG v0.6.0 CACHE STRING "qtpromise tag")

# QtCreator will pass QT_QMAKE_EXECUTABLE automatically
if (DEFINED QT_QMAKE_EXECUTABLE)
    get_filename_component(_QT_USR_DIR ${QT_QMAKE_EXECUTABLE} DIRECTORY)
    get_filename_component(_QT_USR_DIR ${_QT_USR_DIR} DIRECTORY)
    list(APPEND CMAKE_PREFIX_PATH ${_QT_USR_DIR})
    list(APPEND CMAKE_FIND_ROOT_PATH ${_QT_USR_DIR})
    set(_QT_USR_DIR)
endif ()

find_package(QT NAMES Qt6 Qt5 COMPONENTS Core REQUIRED)
find_package(Qt${QT_VERSION_MAJOR} COMPONENTS Core Network REQUIRED)
set(CMAKE_AUTOMOC ON)
set(CMAKE_AUTORCC ON)
set(CMAKE_AUTOUIC ON)

add_compile_definitions(QT_DEPRECATED_WARNINGS)

if (BUILD_STATIC)
    set(LIBRARY_TYPE STATIC)
else ()
    set(LIBRARY_TYPE SHARED)
endif ()

include(FetchContent)
FetchContent_Declare(qtpromise
    GIT_REPOSITORY ${QT_PROMISE_URL}
    GIT_TAG ${QT_PROMISE_TAG}
    GIT_SHALLOW true)
FetchContent_MakeAvailable(qtpromise)

add_subdirectory(src)

if (BUILD_TESTING)
    add_subdirectory(test)
endif()
