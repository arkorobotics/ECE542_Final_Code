cmake_minimum_required(VERSION 2.8)
project( camcv )
SET(COMPILE_DEFINITIONS -Werror)
find_package( OpenCV REQUIRED )
link_directories(/home/pi/pierre/libfacerec-0.04)
include_directories(/opt/vc/userland-master/host_applications/linux/libs/bcm_host/include)
include_directories(/opt/vc/userland-master/host_applications/linux/apps/raspicam/gl_scenes)
include_directories(/opt/vc/userland-master/interface/vcos)
include_directories(/opt/vc/userland-master)
include_directories(/opt/vc/userland-master/interface/vcos/pthreads)
include_directories(/opt/vc/userland-master/interface/vmcs_host/linux)
include_directories(/opt/vc/userland-master/interface/khronos/include)
include_directories(/opt/vc/userland-master/interface/khronos/common)
include_directories(./gl_scenes)
include_directories(.)
add_executable(camcv RaspiCamControl.c RaspiCLI.c RaspiPreview.c camcv.cpp
RaspiTex.c RaspiTexUtil.c
gl_scenes/teapot.c gl_scenes/models.c
gl_scenes/square.c gl_scenes/mirror.c gl_scenes/yuv.c gl_scenes/sobel.c tga.c)
target_link_libraries(camcv /opt/vc/lib/libmmal_core.so
/opt/vc/lib/libmmal_util.so
/opt/vc/lib/libmmal_vc_client.so
/opt/vc/lib/libvcos.so
/opt/vc/lib/libbcm_host.so
/opt/vc/lib/libGLESv2.so
/opt/vc/lib/libEGL.so
/home/pi/pierre/libfacerec-0.04/libopencv_facerec.a
${OpenCV_LIBS}
pthread
-lm)