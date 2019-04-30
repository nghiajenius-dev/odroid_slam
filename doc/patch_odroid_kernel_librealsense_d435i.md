# Notes on using Intel Realsense Camera D435i with Odroid N2 (bionic, kernel 4.9)

## Problems while installing librealsense (Realsense SDK 2.0):
1. Need patch for realsense camera-formats, hid accel & gyro, metadata, and powerline setting
2. IIO module (used for accel and gyro) is not enable in kernel 4.9 config
3. Drop framerate while streamming (not fix)

## Solutions:
### 0. Preparation  
Update:
`sudo apt-get update && sudo apt-get upgrade && sudo apt-get dist-upgrade`

Prepare build environment (if needed, used for patching kernel):  
`sudo apt-get install git libssl-dev libusb-1.0-0-dev pkg-config libgtk-3-dev`
`sudo apt-get install libglfw3-dev libgl1-mesa-dev libglu1-mesa-dev`

### 1. Apply patch to kernel source, and enable IIO module in odroidn2_defconfig: 
Patch applied here:
`https://github.com/nghiajenius-dev/linux/tree/odroidn2-4.9.y_realsense_patch`

### 2. Perform native compile with patched kernel:
Clone the patched kernel and compile:
`https://wiki.odroid.com/odroid-n2/software/building_kernel#native_compile_-_odroid-n2ubuntu
`
### 3. Build librealsense and examples:  
Clone: `https://github.com/IntelRealSense/librealsense`  
`cd librealsense`  
`mkdir build && cd build`  
`cmake ../ -DBUILD_EXAMPLES=true`  
`sudo make uninstall && make clean`  
`make -j4`  
`sudo make install`  

**Build artifacts:**  
- shared object: `/usr/local/lib`  
- header files: `/usr/local/include`  
- binary demos: `/usr/local/bin ` 

### 4. Check for patched kernel (optional):
`sudo modprobe uvcvideo`  
`sudo dmesg`  

### 5. Run applications:
`realsense-viewer`: depth, rgb cameras and imu detected  
`/usr/local/bin/rs-capture`  
`/usr/local/bin/rs-color`  
`/usr/local/bin/rs-depth`  

### 6. Install ROS Melodic
Instruction: `http://wiki.ros.org/melodic/Installation/Ubuntu`  
Verify installation:   
`rosversion -d`  
`rosversion roscpp`  
`rospack find roscpp`  


### 7. Install realsense2_camera (ROS Wrapper) 
Instruction: `https://github.com/intel-ros/realsense`  

### 8. Using ROS
Start ros master: `roscore`  

#### Issue: localhost not recognized
Hostnames are stored in `/etc/hosts`    
Disable IPv6 in Odroid: `https://forum.odroid.com/viewtopic.php?f=112&t=8287`  
`export ROS_MASTER_URI=http://127.0.0.1:11311`  
`export ROS_HOSTNAME=127.0.0.1` 

#### Issue: USB SCP overflow
https://github.com/intel-ros/realsense/issues/669
Workaround:  
`roslaunch realsense2_camera rs_camera.launch filters:=pointcloud enable_infra1:=false enable_infra2:=false`
