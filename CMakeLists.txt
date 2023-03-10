cmake_minimum_required(VERSION 3.16)
project(qmltermwidget VERSION 1.0 LANGUAGES CXX)

set(CMAKE_INCLUDE_CURRENT_DIR ON)

add_definitions(-DHAVE_POSIX_OPENPT -DHAVE_SYS_TIME_H)

find_package(QT NAMES Qt6 REQUIRED COMPONENTS Core)
find_package(Qt${QT_VERSION_MAJOR} REQUIRED COMPONENTS Gui Qml Quick Widgets Core5Compat)

qt_standard_project_setup()

set(plugin_HEADERS
    lib/BlockArray.h
    lib/CharacterColor.h
    lib/Character.h
    lib/ColorScheme.h
    lib/ColorTables.h
    lib/DefaultTranslatorText.h
    lib/Emulation.h
    lib/ExtendedDefaultTranslator.h
    lib/Filter.h
    lib/History.h
    lib/HistorySearch.h
    lib/KeyboardTranslator.h
    lib/konsole_wcwidth.h
    lib/kprocess.h
    lib/kptydevice.h
    lib/kpty.h
    lib/kpty_p.h
    lib/kptyprocess.h
    lib/LineFont.h
    lib/Pty.h
    lib/ProcessInfo.h
    lib/Screen.h
    lib/ScreenWindow.h
    #lib/SearchBar.h
    lib/Session.h
    lib/ShellCommand.h
    lib/TerminalCharacterDecoder.h
    lib/TerminalDisplay.h
    lib/tools.h
    lib/Vt102Emulation.h
    lib/mac-vkcode.h
    #lib/qtermwidget.h
    src/qmltermwidget_plugin.h
    src/ksession.h
    )

set(plugin_SOURCES
    lib/BlockArray.cpp
    lib/ColorScheme.cpp
    lib/Emulation.cpp
    lib/Filter.cpp
    lib/History.cpp
    lib/HistorySearch.cpp
    lib/KeyboardTranslator.cpp
    lib/konsole_wcwidth.cpp
    lib/kprocess.cpp
    lib/kpty.cpp
    lib/kptydevice.cpp
    lib/kptyprocess.cpp
    lib/ProcessInfo.cpp
    lib/Pty.cpp
    #lib/qtermwidget.cpp
    lib/Screen.cpp
    lib/ScreenWindow.cpp
    #lib/SearchBar.cpp
    lib/Session.cpp
    lib/ShellCommand.cpp
    lib/TerminalCharacterDecoder.cpp
    lib/TerminalDisplay.cpp
    lib/tools.cpp
    lib/Vt102Emulation.cpp
    src/qmltermwidget_plugin.cpp
    src/ksession.cpp
    )

qt_add_qml_module(qmltermwidget
    URI QMLTermWidget
    VERSION ${PROJECT_VERSION}
    PLUGIN_TARGET qmltermwidget
    NO_GENERATE_PLUGIN_SOURCE
    SOURCES
        ${plugin_HEADERS} ${plugin_SOURCES}
)

target_include_directories(qmltermwidget PUBLIC
    src lib
)

target_link_libraries(qmltermwidget PUBLIC
    Qt::Core
    Qt::Gui
    Qt::Qml
    Qt::Quick
    Qt::Widgets
    Qt::Core5Compat
)

install(TARGETS qmltermwidget
    RUNTIME DESTINATION "${CMAKE_INSTALL_LIBDIR}/qt${QT_VERSION_MAJOR}/qml/QMLTermWidget"
    BUNDLE DESTINATION "${CMAKE_INSTALL_LIBDIR}/qt${QT_VERSION_MAJOR}/qml/QMLTermWidget"
    LIBRARY DESTINATION "${CMAKE_INSTALL_LIBDIR}/qt${QT_VERSION_MAJOR}/qml/QMLTermWidget"
)

install(DIRECTORY lib/kb-layouts DESTINATION "${CMAKE_INSTALL_LIBDIR}/qt${QT_VERSION_MAJOR}/qml/QMLTermWidget")
install(DIRECTORY lib/color-schemes DESTINATION "${CMAKE_INSTALL_LIBDIR}/qt${QT_VERSION_MAJOR}/qml/QMLTermWidget")
install(FILES 
    src/qmldir
    src/QMLTermScrollbar.qml
    DESTINATION "${CMAKE_INSTALL_LIBDIR}/qt${QT_VERSION_MAJOR}/qml/QMLTermWidget")