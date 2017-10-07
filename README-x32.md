```
# Compile NFC-Tools and libnfc.dll for Windows  # 32-bit version only!  
  
# Tested using windows 10 pro x64, build 1703.  
  
# install latest libusbk release from: (this installs both libusb and libusbk windows components required for running libnfc applications)  
https://sourceforge.net/projects/libusb-win32/files/libusbK-release/  
https://sourceforge.net/projects/libusb-win32/files/libusbK-release/libusbK-3.0.7.0-setup.exe  
  
# install NFC tools compilation toolchain on Windows:  
  
#Install latest version of: MSYS2  for 64-bit windows. (should work fine on 32-bit windows as well)  
# even if msys2 version appears old, the packages it installs are very recent:  
http://www.msys2.org/  
#: msys2-x86_64-xxxxxxxx.exe  
  
  
#Open the MSYS shell in mingw-32 mode (32-bit mode)  
  
#update the MSYS system using pacman:  
pacman -Syu  
  
#close the shell and run:  
pacman -Syyuu  
  
#install build tools:  
pacman -S git make mingw-w64-i686-gcc mingw-w64-i686-binutils mingw-w64-i686-cmake mingw-w64-i686-zlib mingw-w64-i686-make   
  
#restart msys2 bash - in mingw-32 mode.  
  
# this package is used to build against, this version of libusb-win32 is different than the driver package   
#  installed as a prereq above  
  
# download libusb-win32-bin-1.2.6.0   
https://sourceforge.net/projects/libusb-win32/files/libusb-win32-releases/1.2.6.0/  
#extract contents to this directory:  
C:\Program Files (x86)\libusb-win32  
  
  
#download source files:  
cd ~  
mkdir libnfc-build  
git clone https://github.com/libnfc/libnfc.git  
  
# If using the official repo manually update the cmakelists.txt:
# Fix for files that don't build correctly in windows due to "undefined reference" errors:  
# modify this source file:     
~\libnfc\examples\CMakeLists.txt  
#comment out the pn53x-*** entries at the top of the file. this skips them in the build process.  
  
# launch windows powershell x86 (non-admin)  
# add some paths for current build session:  
  
$env:Path += "C:\msys64\mingw32\bin;C:\msys64\mingw32\i686-w64-mingw32\lib;C:\msys64\mingw32\i686-w64-mingw32\include"  
#then, run "CMD.exe"  
cmd.exe  
  
rem create make files:  
  
cd c:\msys64\home\benjamin\libnfc-build  
  
cmake -G "MinGW Makefiles" -DCMAKE_BUILD_TYPE=Release ..\libnfc  
  
# run it again...  
cmake -G "MinGW Makefiles" -DCMAKE_BUILD_TYPE=Release ..\libnfc  
  
mingw32-make  
  
# put compiled DLL file to the system32 directory: (c:\windows\syswow64\libnfc.dll on 64-bit computers!)  
copy .\libnfc\libnfc.dll c:\windows\system32\libnfc.dll  
  
# place libnfc.conf file under:
c:\program files (x86)\libnfc\config\libnfc.conf

```
  
