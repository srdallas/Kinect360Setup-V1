# Setup Skeleton Markers
1. Download the following repos:

`git clone https://github.com/OpenKinect/libfreenect`

`git clone https://github.com/OpenNI/OpenNI`

`git clone https://github.com/arnaud-ramey/NITE-Bin-Dev-Linux-v1.5.2.23`


2. Install the following packages:

`sudo apt-get install cmake freeglut3-dev pkg-config build-essential libxmu-dev libxi-dev libusb-1.0-0-dev python`

`sudo add-apt-repository "deb http://archive.canonical.com/ lucid partner"`

`sudo apt-get update`

`sudo apt-get install doxygen mono-complete graphviz`

3. Install openKinect (libFreenect)

 **in libfreenect directory, in the KinectLibs dir**

`mkdir build`

`cd build`

`cmake ..`

`make`

`sudo make install`

`sudo ldconfig /usr/local/lib64/`

`sudo chmod a+rw /dev/bus/usb//`

`lsusb | grep Xbox`

You should see this:
>Bus 003 Device 005: ID 045e:02ae Microsoft Corp. Xbox NUI Camera
>
>Bus 003 Device 003: ID 045e:02b0 Microsoft Corp. Xbox NUI Motor
>
>Bus 003 Device 004: ID 045e:02ad Microsoft Corp. Xbox NUI Audio

4. Test libfreenect by running

`freenect-glview`

A window like this will appear

`need to put image here`

- We will use libfreenect to control the tilt and the led (so the device Xbox NUI Motor, which also handle the led).

- We will use OpenNi + Sensor module to get the camera streams (the device Xbox NUI Camera)

- We will use NITE libraries in concert with OpenNI to get the high level API (so gesture recognition, hand/skeleton tracking and so on)


5. Install OpenNi

**In OpenNI directory**

`cd Platform/Linux/CreateRedist`

`chmod +x ./RedistMaker`

`./RedistMaker`

`sudo ./install.sh`

If you see the process is failed, don’t panic. That’s OK.

6. Install NITE

`cd NITE-Bin-Dev-Linux-v1.5.2.23/x64`

`sudo sh install.sh`

7. Install skeleton_markers ROS package

`cd catkin_ws/src`

`git clone https://github.com/pirobot/skeleton_markers`

`cd ..`

`catkin_make`

`source devel/setup.bash`

`roscore`

`roslaunch skeleton_markers markers.launch`


This window should appear:

`insert image here`

Enjoy
