# Create the config.h header file
configure_file(
    "${CMAKE_CURRENT_SOURCE_DIR}/config.h.in"
    "${CMAKE_CURRENT_BINARY_DIR}/config.h" @ONLY
)

file(GLOB_RECURSE QML_SOURCES
    "${CMAKE_CURRENT_SOURCE_DIR}/qml/*.qml"
    "${CMAKE_CURRENT_SOURCE_DIR}/qml/*.js")

set(SOURCES
    main.cpp
)

qt5_add_resources(RESOURCES files.qrc)

add_executable(liri-files ${SOURCES} ${QML_SOURCES} ${RESOURCES})
target_link_libraries(liri-files
                      Qt5::Qml
                      Qt5::QuickControls2)

install(TARGETS liri-files
        DESTINATION ${BIN_INSTALL_DIR})
install(FILES io.liri.Files.desktop
        DESTINATION ${XDG_APPS_INSTALL_DIR})
