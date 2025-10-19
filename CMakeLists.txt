cmake_minimum_required(VERSION 3.22)
project(enb-api VERSION 1.0.0 LANGUAGES CXX)

# Header-only library
add_library(enb-api INTERFACE)
add_library(enb-api::enb-api ALIAS enb-api)

target_include_directories(enb-api INTERFACE
    $<BUILD_INTERFACE:${CMAKE_CURRENT_SOURCE_DIR}>
    $<INSTALL_INTERFACE:${CMAKE_INSTALL_INCLUDEDIR}>
)

# Installation
include(GNUInstallDirs)
install(FILES
    ENBSeriesAPI.h
    ENBSeriesSDK.h
    AntTweakBar.h
    DESTINATION ${CMAKE_INSTALL_INCLUDEDIR}
)

install(TARGETS enb-api
    EXPORT enb-api-targets
)

install(EXPORT enb-api-targets
    FILE enb-api-config.cmake
    NAMESPACE enb-api::
    DESTINATION ${CMAKE_INSTALL_LIBDIR}/cmake/enb-api
)
