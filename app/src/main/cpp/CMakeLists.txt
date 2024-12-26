
cmake_minimum_required(VERSION 3.22.1)

project("android_tutorial_1")

# Set the GStreamer root path
if(NOT DEFINED ENV{GSTREAMER_ROOT_ANDROID})
    message(FATAL_ERROR "GSTREAMER_ROOT_ANDROID is not defined!")
endif()
set(GSTREAMER_ROOT $ENV{GSTREAMER_ROOT_ANDROID})

# Set the GStreamer NDK build path
set(GSTREAMER_NDK_BUILD_PATH ${GSTREAMER_ROOT}/share/gst-android/ndk-build/)

# Specify the GStreamer plugins and extra dependencies
set(GSTREAMER_PLUGINS coreelements ogg theora vorbis videoconvert audioconvert audioresample playback glimagesink soup opensles)
set(G_IO_MODULES gnutls)
set(GSTREAMER_EXTRA_DEPS gstreamer-video-1.0)

add_library(${CMAKE_PROJECT_NAME} SHARED
        # List C/C++ source files with relative paths to this CMakeLists.txt.
        native-lib.cpp)



target_link_libraries(${CMAKE_PROJECT_NAME}
        # List libraries link to the target library
        # GStreamer::mobile
        android
        log)