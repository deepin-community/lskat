ecm_setup_version(${LSKAT_VERSION}
    VARIABLE_PREFIX LSKAT
    VERSION_HEADER lskat_version.h
)

configure_file(config-src.h.in ${CMAKE_CURRENT_BINARY_DIR}/config-src.h)

add_executable(lskat)

target_sources(lskat PRIVATE
    thememanager.cpp
    namedialogwidget.cpp
    gameview.cpp
    mainwindow.cpp
    main.cpp
    deck.cpp
    config_two.cpp
    abstractdisplay.cpp
    display_intro.cpp
    display_two.cpp
    cardsprite.cpp
    pixmapsprite.cpp
    scoresprite.cpp
    textsprite.cpp
    abstractengine.cpp
    engine_two.cpp
    player.cpp
    abstractinput.cpp
    mouseinput.cpp
    aiinput.cpp
    fromlibkdegames/cardcache.cpp
    fromlibkdegames/carddeckinfo.cpp
    fromlibkdegames/kcarddialog.cpp

    lskat.qrc
)

ki18n_wrap_ui(lskat
    namedialog.ui
    fromlibkdegames/kgamecardselector.ui
)

# Debug as default severity, at least until global_debug is removed
ecm_qt_declare_logging_category(lskat
    HEADER lskat_debug.h
    IDENTIFIER LSKAT_LOG
    CATEGORY_NAME org.kde.lskat
    DEFAULT_SEVERITY Debug
    DESCRIPTION "LSkat game"
    EXPORT LSKAT
)

file(GLOB ICONS_SRCS "${CMAKE_CURRENT_SOURCE_DIR}/../*-apps-lskat.png")
ecm_add_app_icon(lskat ICONS ${ICONS_SRCS})

target_link_libraries(lskat
    KF5KDEGames
    KF5::Crash
    KF5::GuiAddons
    KF5::XmlGui
    Qt::Gui
    Qt::Svg
)

install(TARGETS lskat  ${KDE_INSTALL_TARGETS_DEFAULT_ARGS})

ecm_qt_install_logging_categories(
    EXPORT LSKAT
    FILE lskat.categories
    DESTINATION ${KDE_INSTALL_LOGGINGCATEGORIESDIR}
)
