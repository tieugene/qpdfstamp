cmake_minimum_required(VERSION 3.19)
project(qpdfstamp LANGUAGES CXX)

find_package(Qt6 6.5 REQUIRED COMPONENTS Core Widgets LinguistTools)

qt_standard_project_setup()

qt_add_executable(qpdfstamp
    WIN32 MACOSX_BUNDLE
    src/main.cpp
    src/mainwindow.cpp
    src/mainwindow.h
)

qt_add_translations(
    TARGETS qpdfstamp
    TS_FILES src/ts/qpdfstamp_ru_RU.ts
)

target_link_libraries(qpdfstamp
    PRIVATE
        Qt::Core
        Qt::Widgets
)

install(TARGETS qpdfstamp
    BUNDLE  DESTINATION .
    RUNTIME DESTINATION ${CMAKE_INSTALL_BINDIR}
    LIBRARY DESTINATION ${CMAKE_INSTALL_LIBDIR}
)

qt_generate_deploy_app_script(
    TARGET qpdfstamp
    OUTPUT_SCRIPT deploy_script
    NO_UNSUPPORTED_PLATFORM_ERROR
)
install(SCRIPT ${deploy_script})
