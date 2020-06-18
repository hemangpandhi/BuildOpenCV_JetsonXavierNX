# BuildOpenCV_JetsonXavierNX

Build OpenCV 4.4.0 (Pre release version) with CUDA support enabled on Jetson Xavier NX

Step 1: Update the dependacies using below command.
sudo apt-get update

Step 2: Install required dependacies to build OpenCV using apt-get commands.

sudo apt install gcc-6 g++-6 cmake build-essential git pkg-config ccache \
unzip ecm extra-cmake-modules fcitx-libs-dev libfcitx-qt5-1 \
mesa-utils libgtk2.0-dev libgtk-3-dev ffmpeg \
libavcodec-dev libavformat-dev libswscale-dev \
libjpeg-dev libpng-dev libtiff5-dev x264 libxvidcore-dev yasm \
libxine2-dev libv4l-dev libfaac-dev libmp3lame-dev libopencore-amrnb-dev \
libopencore-amrwb-dev libtheora-dev libvorbis-dev libxvidcore-dev \
x264 v4l-utils ffmpeg libdc1394-22 libdc1394-22-dev libtiff5-dev \
qt5-default libeigen3-dev libeigen3-doc tesseract-ocr tesseract-ocr-jpn \
vtk6 tcl-vtk6 python-vtk6 libgflags-dev autoconf automake libtool \
autoconf-archive libleptonica-dev libtesseract-dev gphoto2 liblapacke-dev \
libgoogle-glog-dev libprotobuf-dev libprotoc-dev protobuf-compiler \
libgphoto2-dev libvtk6-dev libvtk6-qt-dev liblapack-dev libatlas-base-dev

Step 3: Clone OpenCV source code from OpenCV repository
git clone https://github.com/opencv/opencv.git
git clone https://github.com/opencv/opencv_contrib.git

Note: Above command will fetch the source code from the master branch, If you want to build with release branch, kindly change
the branch after fetching the source code.

Step 4: Change directory to OpenCV
cd opencv

Step 5: Create build directory and move to build directory
mkdir build
cd build

Step 6: Configure OpenCV modules and enable CUDA support for OpenCV using Cmake commands and generate the Makefile.
cmake -D CUDNN_VERSION='8.0' -D WITH_CUDA=ON -D CUDA_FAST_MATH=ON -D WITH_CUBLAS=ON -D WITH_CUDNN=ON -D CUDA_ARCH_BIN=7.2 -D CUDA_ARCH_PTX=7.2 -D CUDA_ARCH_PTX="" -D OPENCV_DNN_CUDA=ON -D OPENCV_GENERATE_PKGCONFIG=ON -D CUDNN_INCLUDE_DIR=/usr/include -D OPENCV_EXTRA_MODULES_PATH=../../opencv_contrib/modules -D WITH_GSTREAMER=ON -D WITH_LIBV4L=ON -D BUILD_opencv_python3=ON -D BUILD_TESTS=OFF -D BUILD_PERF_TESTS=OFF -D BUILD_EXAMPLES=OFF -D CMAKE_BUILD_TYPE=RELEASE -D CMAKE_INSTALL_PREFIX=/usr/local ..

Step 7: Build OpenCV using make command.
make -j4

Step 8: Install OpenCV module using make install command.
sudo make install

Step 9: Verify whether CUDA support is enabled or not using following command.
Open new terminal
Type python
>> import cv2
>> cv2.cuda.getCudaEnabledDeviceCount()

CUDA support is enabled if the CudaEnabledDeviceCount is non zero.

You can also verify whether CUDA support is enabled or not using jtop command.
-> Open terminal
-> open jtop
-> Go to Info by pressing 6 key.
-> Verify the OpenCV libraries (Compiled CUDA flag should be YES)
