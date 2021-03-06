project(cyber-session)
set(TARGET cyber-session)

set(SOURCES
    application.cpp
    main.cpp
    process.cpp
    processmanager.cpp

    powermanager/power.cpp
    powermanager/powerproviders.cpp
)

qt5_add_dbus_adaptor(DBUS_SOURCES
                     org.cyber.Session.xml
                     application.h Application
                     sessionadaptor SessionAdaptor)
set_source_files_properties(${DBUS_SOURCES} PROPERTIES SKIP_AUTOGEN ON)

add_executable(${TARGET} ${SOURCES} ${DBUS_SOURCES})
target_link_libraries(${TARGET}
        Qt5::Core
        Qt5::Gui
        Qt5::Widgets
        Qt5::DBus
)

install(TARGETS ${TARGET} DESTINATION /usr/bin)
install(FILES cyber-xsession.desktop DESTINATION /usr/share/xsessions/)
