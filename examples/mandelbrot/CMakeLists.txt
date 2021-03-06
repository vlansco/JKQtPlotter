cmake_minimum_required(VERSION 3.0)

set(EXAMPLE_NAME mandelbrot)
set(EXENAME jkqtptest_${EXAMPLE_NAME})

message( STATUS "..   Building Example ${EXAMPLE_NAME}" )

find_package(Threads REQUIRED)

# Set up source files
set(SOURCES ${EXAMPLE_NAME}.cpp mandelbrotmainwindow.cpp)
set(HEADERS mandelbrotmainwindow.h)
set(RESOURCES  )
set(UIS  mandelbrotmainwindow.ui)

add_executable(${EXENAME} WIN32 ${SOURCES} ${HEADERS} ${RESOURCES} ${UIS})
target_include_directories(${EXENAME} PRIVATE ../../lib)
if(JKQtPlotter_BUILD_STATIC_LIBS)
    target_link_libraries(${EXENAME} JKQTPlotterLib)
elseif(JKQtPlotter_BUILD_SHARED_LIBS)
    target_link_libraries(${EXENAME} JKQTPlotterSharedLib)
endif()
target_link_libraries(${EXENAME} Threads::Threads)


# Installation
install(TARGETS ${EXENAME} RUNTIME DESTINATION ${CMAKE_INSTALL_BINDIR})

#Installation of Qt DLLs on Windows
jkqtplotter_deployqt(${EXENAME})
