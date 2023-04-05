cmake_minimum_required(VERSION 3.15)
project(libspatter VERSION 0.0.1 DESCRIPTION "generate memory access patterns")

# Create an install rule
include(GNUInstallDirs)

add_library(libspatter SHARED
    #src/generatorBase.cc
    #src/uniformGenerator.cc
    src/spatter.cc
)

set_target_properties(libspatter PROPERTIES
    VERSION ${PROJECT_VERSION}
    SOVERSION 1
    PUBLIC_HEADER include/spatter.h)

configure_file(libspatter.pc.in libspatter.pc @ONLY)

# Make files avilable without needing relative paths
target_include_directories(mylib PRIVATE .)

# Declare files to install
install(TARGETS libspatter
    LIBRARY DESTINATION ${CMAKE_INSTALL_LIBDIR}
    PUBLIC_HEADER DESTINATION ${CMAKE_INSTALL_INCLUDEDIR})

install(FILES ${CMAKE_BINARY_DIR}/libspatter.pc DESTINATION ${CMAKE_INSTALL_DATAROOTDIR}/pkgconfig)
