set(CMAKE_AUTOMOC OFF)

set(MODULE_NAME QtOffscreenViews)

set(SRC_LIST
    QAndroidJniImagePair.cpp
    QAndroidJniImagePair.h
    QAndroidOffscreenEditText.cpp
    QAndroidOffscreenEditText.h
    QAndroidOffscreenView.cpp
    QAndroidOffscreenView.h
    QAndroidOffscreenWebView.cpp
    QAndroidOffscreenWebView.h
    QApplicationActivityObserver.cpp
    QApplicationActivityObserver.h
    QOpenGLTextureHolder.cpp
    QOpenGLTextureHolder.h
#    QGraphicsWidgets/QAndroidOffscreenViewGraphicsWidget.cpp
#    QGraphicsWidgets/QAndroidOffscreenViewGraphicsWidget.h
#    QGraphicsWidgets/QOffscreenEditTextGraphicsWidget.cpp
#    QGraphicsWidgets/QOffscreenEditTextGraphicsWidget.h
#    QGraphicsWidgets/QOffscreenWebViewGraphicsWidget.cpp
#    QGraphicsWidgets/QOffscreenWebViewGraphicsWidget.h
    QQuickViews/QQuickAndroidOffscreenView.cpp
    QQuickViews/QQuickAndroidOffscreenView.h
    QQuickViews/QQuickOffscreenEditText.cpp
    QQuickViews/QQuickOffscreenEditText.h
    QQuickViews/QQuickOffscreenWebView.cpp
    QQuickViews/QQuickOffscreenWebView.h
)

if (ANDROID)
    qt5_wrap_cpp(
        QtOffscreenViews_hdr_moc
        QAndroidJniImagePair.h
        QAndroidOffscreenEditText.h
        QAndroidOffscreenView.h
        QAndroidOffscreenWebView.h
        QApplicationActivityObserver.h
        QQuickViews/QQuickAndroidOffscreenView.h
        QQuickViews/QQuickOffscreenEditText.h
        QQuickViews/QQuickOffscreenWebView.h
    )

    find_library(ANDROID_JNIGRAPHICS jnigraphics)
    add_library(${MODULE_NAME} STATIC ${SRC_LIST} ${QtOffscreenViews_hdr_moc})
    add_library(${PROJECT_NAME}::${MODULE_NAME} ALIAS ${MODULE_NAME})

    target_link_libraries(${MODULE_NAME}
        PUBLIC
            Qt5::Core
            Qt5::Gui
            qtandroidextensions::QtJniHelpers
        PRIVATE
            Qt5::OpenGL
            Qt5::Qml
            Qt5::Quick
            ${ANDROID_JNIGRAPHICS}
    )

    target_include_directories(${MODULE_NAME}
        PUBLIC
            ${PROJECT_SOURCE_DIR}
        PRIVATE
            ${CMAKE_CURRENT_SOURCE_DIR}
    )
endif(ANDROID)

