# Kinect360Setup-V1

starting here https://www.kdab.com/setting-up-kinect-for-programming-in-linux-part-1/

1. Envrionment Setup

This command : sudo add-apt-repository "deb http://archive.canonical.com/ lucid partner"

change to this:   sudo add-apt-repository "deb http://archive.canonical.com/ bionic partner"

This reason is that the lucid or bionic keyword changes depending on your Ubuntu version, the one I used was 18.04 which is known as bionic beaver.
	
For the java line that fails I used this to install java https://www.digitalocean.com/community/tutorials/how-to-install-java-with-apt-on-ubuntu-18-04 

I am not entirely sure if Java is needed for this to work but I will do so to preemptively handle any errors. Note: I installed both the JRE and the JDK.

1. Install openKinect (libFreenect)	

Everything here should work fine except for when they tell you to test it. Because you had to install libfreenect the command to test it is not `glview` but `freenect-glview`.

DO NOT DO PART 2. Install OpenNi	
I would stop here because this is when things start to be deprecated and instead we are going to go on our own to install the rest. Such that we will eventually have ros running with a skeleton marker program.

getting error build failed on running command ./RedistMaker

fix was found using this: https://github.com/OpenNI/OpenNI/issues/26 
if you don’t want to read the thread just run these commands: 

sudo apt-get install mono-complete
sudo apt install gcc-4.8 g++-4.8
sudo apt install clang-3.9 clang-4.0

sudo update-alternatives --install /usr/bin/gcc gcc /usr/bin/gcc-7 10
sudo update-alternatives --install /usr/bin/g++ g++ /usr/bin/g++-7 10
sudo update-alternatives --install /usr/bin/gcc gcc /usr/bin/gcc-4.8 20
sudo update-alternatives --install /usr/bin/g++ g++ /usr/bin/g++-4.8 20
echo "alias clang++=\"clang++-3.5\"" >> .bashrc
(not sure if this line even does anything) export CXX=clang++ yaourt -S openni
sudo apt install clang

NOTE: After this section or later when you finish you will need to redo this line but as this:

sudo update-alternatives --install /usr/bin/gcc gcc /usr/bin/gcc-7 20
sudo update-alternatives --install /usr/bin/g++ g++ /usr/bin/g++-7 20
sudo update-alternatives --install /usr/bin/gcc gcc /usr/bin/gcc-4.8 10
sudo update-alternatives --install /usr/bin/g++ g++ /usr/bin/g++-4.8 10
after running all of those commands aside from the NOTE 
do this command: sudo ./RedistMaker
fixed this error with this https://www.oreilly.com/library/view/kinect-hacks/9781449332181/ch01.html 
https://anwiki.artsaucarre.be/index.php?title=OpenNI_and_NITE_on_linux 
commands to run:
cd KinectLibs/OpenNI/Platform/Linux/Redist/OpenNI-Bin-Dev-Linux-x64-v1.5.4.0/
sudo ./install.sh	

$ cd SensorKinect
$ cd Platform/Linux/CreateRedist
$ chmod +x RedistMaker
$ ./RedistMaker
$ cd ../Redist/Sensor-Bin-Linux-[xxx] (where [xxx] is your architecture and this particular OpenNI release)
$ chmod +x install.sh
$ sudo ./install.sh

also git cloned this is https://github.com/arnaud-ramey/NITE-Bin-Dev-Linux-v1.5.2.23 and followed the commands in its read.me

NOW OpenNI User tracking should be working just fine

--ROS section--

git clone these two into your src folder

git clone https://github.com/pirobot/skeleton_markers

git clone https://github.com/ros-drivers/openni_camera

cd ..

catkin_make

open a new terminal

run roscore

go back to original terminal

source devel/setup.bash

roslaunch skeleton_markers skeleton.tracker
