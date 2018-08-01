## Tested Hardware and Software Setting by pjinkim

*   Environments: Ubuntu 14.04.5 LTS (64-bit) + Kinect v1 for Windows (Model 1517) + MSI Laptop (GS60 Ghost pro)


## 1. Install OpenNI-Unstable-1.5.4.0
Please, refer to https://codeyarns.com/2013/07/23/how-to-get-started-with-kinect-for-windows-on-ubuntu-using-openni/ and https://github.com/OpenNI/OpenNI/tree/Unstable-1.5.4.0 and follow the below instructions.

Requirements
```
$ sudo apt-get install terminator git git-cola build-essential cmake vim
$ sudo apt-get install g++ python
$ sudo apt-get install libusb-1.0-0-dev
$ sudo apt-get install freeglut3-dev
$ sudo apt-get install openjdk-6-jdk
$ sudo apt-get install doxygen
$ sudo apt-get install graphviz
$ sudo apt-get install mono-complete
```

Compile the OpenNI code
```
$ cd OpenNI-Unstable-1.5.4.0/
$ cd Platform/Linux/CreateRedist/
$ ./RedistMaker
```

Install the OpenNI headers, libraries and binaries on the system
```
$ cd ../Redist/
$ cd OpenNI-Bin-Dev-Linux-x64-v1.5.4.0/
$ sudo ./install.sh
```

You now have OpenNI installed. However, it cannot yet communicate with your Kinect for Windows sensor. To get that working, we need to install the Kinect drivers.


## 2. Install SensorKinect-unstable drivers
Please, refer to https://codeyarns.com/2013/07/23/how-to-get-started-with-kinect-for-windows-on-ubuntu-using-openni/ and https://stackoverflow.com/questions/28319336/xndevicesensorv2-failed-on-raspberry-pi and https://groups.google.com/forum/#!topic/openni-dev/LZpcyCfh9UE and follow the below instructions.

Compile the SensorKinect driver code
```
$ cd SensorKinect-unstable/
$ cd Platform/Linux/CreateRedist/
$ ./RedistMaker
```

Install the SensorKinect drivers
```
$ cd ../Redist/
$ cd Sensor-Bin-Linux-x64-v5.1.2.1/
$ sudo ./install.sh
```

You now have the drivers installed on your system.
Start playing with Kinect
```
$ sudo modprobe -r gspca_kinect
$ sudo sh -c 'echo "blacklist gspca_kinect" > /etc/modprobe.d/blacklist-kinect.conf'
$ cd Documents/OpenNI-Unstable-1.5.4.0/Platform/Linux/Bin/x64-Release/
$ ./NiViewer
```

For example, the NiViewer tool displays both the RGB and depth output from your Kinect.


## 3. Install & Build opencv-2.4.9 with OpenNI
Please, refer to https://github.com/PyojinKim/xtionpro_sample_applications/blob/master/note2_opencv_withopenni.pdf and https://docs.opencv.org/2.4.13/doc/user_guide/ug_kinect.html and follow the below instructions.

Requirements
```
$ sudo apt-get install libgtk2.0-dev cmake-qt-gui
```

Compile OpenCV-2.4.9 with <WITH_OPENNI=ON> & <WITH_GTK=ON>
```
$ cd opencv-2.4.9/
$ mkdir build
$ cmake-gui
```
for cmake-gui,
The installation steps as follows,
Where is the source code : /home/pjinkim/opencv-2.4.9
Where to build the binaries : /home/pjinkim/opencv-2.4.9/build

Configure (Unix Makefiles) and check <WITH_OPENNI> and Configure again.

Make sure that the folders to OpenNI and Kinect drivers are correct and click configure again. If everything is fine then there will be no entries marked in red. To make sure that the build is configured properly with OpenNI, see the OPENNI field in the output window, it should say YES and should be configured with SensorKinect drivers.
Now finally click Generate.

```
$ cd opencv-2.4.9/build
$ make -j4
$ sudo make install
$ pkg-config --modversion opencv
```


## 4. Run simple example (Kinect4Windows_sensor_interface)

Run
```
$ cd Kinect4Windows_sensor_interface/
$ mkdir build
$ cd build
$ cmake ..
$ make -j4
$ ./Kinect4Windows_sensor_interface
```



