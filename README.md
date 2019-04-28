# ODROID SLAM
This repository contains configurations to build SLAM application on Odroid N2  
- Odroid Forum: https://forum.odroid.com/viewforum.php?f=175  
- Odroid Wiki: https://wiki.odroid.com/odroid-n2/odroid-n2  

## 1. Flash ubuntu minimal image  
Images: https://wiki.odroid.com/odroid-n2/os_images/ubuntu/20190329
> Notes: During 1st boot, RootFS auto-resize feature will run, then the board will shut off. Wait for a few minutes, Re-power the board, system should boot up normally now.

## 2. Update system and kernel software
> sudo apt update  
> sudo apt upgrade  
> sudo apt dist-upgrade  
> sudo reboot  

## Q&A
What is PPSSPP?  
- PSP Emulator (gaming)  
Mate vs Minimal image?  
- Mate: full desktop GUI  
- Minimal: command-line only system  
- Ref: https://forum.odroid.com/viewtopic.php?f=177&t=34608  
OpenCL vs OpenGL?  
- OpenCL(Computer Language): Programming framework for CPU,GPU,DSP,FPGA; for parallel programming  
- OpenGL(Graphics Library): API for rendering 2D/3D vector graphics; interact with GPU to achieve   hw-accelerated rendering

xorg? startx?  
graphical client Cantata?  
Linux Kernel 4.9 vs 4.14 LTS?  
Install GUI on Minimal Ubuntu?  
https://askubuntu.com/questions/142168/how-to-add-applications-and-gui-to-the-minimal-ubuntu  


## Useful Links  
Flash Tool: https://www.balena.io/etcher/  
Sublime Merge: https://www.sublimemerge.com/docs/linux_repositories#apt  
Markdown Syntax:  
https://www.markdownguide.org/basic-syntax/  
https://en.support.wordpress.com/markdown-quick-reference/  


## Useful Commands  
Find linux kernel version: https://www.cyberciti.biz/faq/find-print-linux-unix-kernel-version/  
>> uname -a  
>> cat /proc/version  
>> hostnamectl  
>> lsb_release -a  




