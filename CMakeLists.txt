cmake_minimum_required(VERSION 3.8)
project(webrtc_native_simple_app)
# TODO SUPPORT WINDOWS AND LINUX

if (NOT CMAKE_BUILD_TYPE)
message(STATUS "No build type selected, default to Debug")
set(CMAKE_BUILD_TYPE "Debug")
endif()

set(CMAKE_CXX_STANDARD 14)
set(CMAKE_CXX_FLAGS_DEBUG "${CMAKE_CXX_FLAGS_DEBUG} -g -Wall -Wextra -pedantic -Wcast-align -Wuninitialized -D__STDC_CONSTANT_MACROS -D_GLIBCXX_USE_CXX11_ABI=0 -DWEBRTC_POSIX -DWEBRTC_MAC")
set(CMAKE_CXX_FLAGS_RELEASE "${CMAKE_CXX_FLAGS_RELEASE} -Wall -D__STDC_CONSTANT_MACROS -D_GLIBCXX_USE_CXX11_ABI=0 -DWEBRTC_POSIX -DWEBRTC_MAC")

# Thread
find_package(Threads REQUIRED)

# Webrtc
include_directories(${CMAKE_CURRENT_SOURCE_DIR}/deps/webrtc/include)
if(CMAKE_BUILD_TYPE MATCHES Debug)
set(WEBRTC_LIBRARIES ${CMAKE_CURRENT_SOURCE_DIR}/deps/webrtc/lib/Debug/libwebrtc_full.a)
else()
set(WEBRTC_LIBRARIES ${CMAKE_CURRENT_SOURCE_DIR}/deps/webrtc/lib/Release/libwebrtc_full.a)
message("Release build.")
endif()

add_executable(simple_app simple_app.cc)

target_link_libraries(simple_app
                      ${CMAKE_THREAD_LIBS_INIT}
                      ${WEBRTC_LIBRARIES}
                      "-framework Cocoa"
                      "-framework Foundation"
                      "-framework IOKit"
                      "-framework Security"
                      "-framework SystemConfiguration"
                      "-framework ApplicationServices"
                      "-framework CoreServices"
                      "-framework CoreVideo"
                      "-framework CoreAudio"
                      "-framework AudioToolbox"
                      "-framework QTKit"
                      "-framework AVFoundation"
                      "-framework CoreMedia"
                      )