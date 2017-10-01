# quick_start_webrtc_native
a demo of use webrtc native on macOs with cmake

BIN AND LIB Webrtc for Mac. For Learning use Webrtc Native Api On Mac OS
USE
## build unix project
mkdir -p build && cd build && cmake .. && make -j4
./simple_app

OR:

## build xcode project
mkdir -p xcode && cd xcode && cmake .. -G Xcode
open xcode build
run simple_app