cmake_minimum_required(VERSION 3.15)

project(c4h_md5 VERSION 1.0.0 LANGUAGES CXX)

include(GNUInstallDirs)
include(CMakePackageConfigHelpers)

add_library(c4h_md5 SHARED edm_md5.cc)

add_library(c4h_md5::c4h_md5 ALIAS c4h_md5)

target_include_directories(c4h_md5
    PUBLIC
        $<BUILD_INTERFACE:${CMAKE_CURRENT_SOURCE_DIR}>
        $<INSTALL_INTERFACE:${CMAKE_INSTALL_INCLUDEDIR}>
)

set_target_properties(c4h_md5 PROPERTIES
    OUTPUT_NAME c4h_md5
    PUBLIC_HEADER edm_md5.h
)

install(TARGETS c4h_md5
    EXPORT c4h_md5Targets
    LIBRARY DESTINATION ${CMAKE_INSTALL_LIBDIR}
    ARCHIVE DESTINATION ${CMAKE_INSTALL_LIBDIR}
    RUNTIME DESTINATION ${CMAKE_INSTALL_BINDIR}
    PUBLIC_HEADER DESTINATION ${CMAKE_INSTALL_INCLUDEDIR}
)

install(EXPORT c4h_md5Targets
    FILE c4h_md5Targets.cmake
    NAMESPACE c4h_md5::
    DESTINATION ${CMAKE_INSTALL_LIBDIR}/cmake/c4h_md5
)

configure_package_config_file(
    ${CMAKE_CURRENT_SOURCE_DIR}/cmake/c4h_md5Config.cmake.in
    ${CMAKE_CURRENT_BINARY_DIR}/c4h_md5Config.cmake
    INSTALL_DESTINATION ${CMAKE_INSTALL_LIBDIR}/cmake/c4h_md5
)

write_basic_package_version_file(
    ${CMAKE_CURRENT_BINARY_DIR}/c4h_md5ConfigVersion.cmake
    VERSION ${PROJECT_VERSION}
    COMPATIBILITY SameMajorVersion
)

install(FILES
    ${CMAKE_CURRENT_BINARY_DIR}/c4h_md5Config.cmake
    ${CMAKE_CURRENT_BINARY_DIR}/c4h_md5ConfigVersion.cmake
    DESTINATION ${CMAKE_INSTALL_LIBDIR}/cmake/c4h_md5
)
