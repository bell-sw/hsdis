#Building hsdis.so on Raspberry Pi and others
To build an aarch64 hsdis.so, Pi 3 with OpenSuSE (aarch64 variant) is required

On the Pi, download the following GNU source packages: m4 (fresh version for bison), bison, texinfo, binutils

* http://ftp.gnu.org/gnu/m4/m4-1.4.tar.gz
* http://ftp.gnu.org/gnu/bison/bison-3.0.tar.gz
* http://ftp.gnu.org/gnu/texinfo/texinfo-6.3.tar.gz
* http://ftp.gnu.org/gnu/binutils/binutils-2.28.tar.gz

Scp to pi and unpack them, then install m4, bison, texinfo, but not binutils:

1. cd ...
2. ./configure
3. make                                      ## on amd64 it'll probably require "make all64" instead
4. sudo make install
5.  scp openjdk 9 source tree tip e.g. to get snapshot from cross-build tree use
zip -9 -r --exclude=*.hg* --exclude=*build* open9.zip open9
6. unpack jdk sources
7. unpack binutils as hotspot/src/share/tools/hsdis/build/binutils
8. build the library
9. cd hotspot/src/share/tools/hsdis
10. make

Get the image in build/linux-aarch64/

#Known issues
##Raspbian 

'sudo make install' of m4 may not work, workaround is to install it elsewhere:

m4
./configure --prefix=/home/pi/m4bin

bison
./configure M4=/home/pi/m4bin/bin/m4
