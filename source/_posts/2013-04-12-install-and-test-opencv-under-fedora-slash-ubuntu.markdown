---
layout: post
title: "Install and Test OpenCV under Fedora/Ubuntu"
date: 2013-04-12 19:36
comments: true
categories: software
---

Recently, I attempted to install OpenCV in my laptop for  computer vision course. And I encountered some  problems during the process, but  finally  succeeded!
Here, I will briefly describe what I have done for the installation.
Important: make sure that the following packages have been installed

```
yum list  packagename  # have a look at installed packages
```
<!--more-->
In Fedora 16 ,  the corresponding packages are `gtk2, pkgconfig` respectively
Dowload opencv source code (set 2.4.0 for instance) and uncompress it to your prefered directory:

```
cd  your directory which will contain the source file
tar -xvf  OpenCV-2.4.0.tar.bz2
```
Next, go into the directory of OpenCV and establish a folder named release and enter it:

```
cd  ~/OpenCV-2.4.0/
mkdir release
cd release
```
Now we are under the release folder and execute the following commands:

```
cmake -D CMAKE_BUILD_TYPE=RELEASE -D CMAKE_INSTALL_PREFIX=/usr/local -D BUILD_PYTHON_SUPPORT=ON ..
```
This piece of code will produce makefiles for further processes. Then, we will enter codes in the terminal:

```
make
sudo make install
```
If you have completed above steps,  some configurations should be made for correct use of OpenCV:

```
sudo vim  /etc/ld.so.conf.d/opencv.conf
add /usr/local/lib into the file
sudo ldconfig
```
Furthermore, modify the path variable:

```
sudo vim /etc/profile
add following contents
export PKG_CONFIG_PATH=/usr/local/lib/pkgconfig
export LD_LIBRARY_PATH=/usr/local/lib
```

Save the file and quit, and have modifications come into practice now
or   ` source /etc/profile `
If these methods can not work,  you can logout and enter the system again.
The next part is to test whether openCV can function well.

```
cd ~/OpenCV-2.4.0/samples/c
sh  build_all.sh
./facedetect  lena.jpg
```
If an image can pop up,  congratulations!  The library can work well!
_Notes_:
I have once got a problem when I try to test OpenCV:

`OpenCV Error: Unspecified error (The function is not implemented. Rebuild the library with Windows, GTK+ 2.x or Carbon support. If you are on Ubuntu or Debian, install libgtk2.0-dev and pkg-config, then re-run cmake or configure script) in cvNamedWindow`

I have the gtk2 installed, but the problem still remains.
And then I install the latest version of OpenCV source code. The problem have disappeared!!
OpenCV: old version is 2.3.1, and the current version is 2.4.0.

_References_:

 *  <http://opencv.willowgarage.com/wiki/InstallGuide>

 *  <http://opencv.willowgarage.com/wiki/CompileOpenCVUsingLinux>
