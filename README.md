s2png — “stuff to PNG”
======================

[![Build Status](https://travis-ci.org/dbohdan/s2png.svg)](https://travis-ci.org/dbohdan/s2png)
[![AppVeyor CI build status](https://ci.appveyor.com/api/projects/status/github/dbohdan/s2png?branch=master&svg=true)](https://ci.appveyor.com/project/dbohdan/s2png)

This program stores arbitrary binary data inside PNG images and extracts it back. It was originally developed by k0wax at <http://sourceforge.net/projects/s2png/>. The present version was created to fix a libgd-related problem that caused s2png 0.01 to segfault when compiled on modern GNU/Linux distributions. It has other improvements but remains compatible with the original.

s2png is licensed under the GNU GPL 2.0. See the file LICENSE.

Building and installing
-----------------------

### *nix

1\. Install the dependencies. On Debian, Ubuntu and Linux Mint you can do so with
`sudo apt-get install libgd2-noxpm libgd2-noxpm-dev`. On FreeBSD install `graphics/gd`.

2\. Clone the repository and `cd` into it.

```sh
git clone https://github.com/dbohdan/s2png
cd s2png/
```

3\. Run `make`. Building has been tested on the following operating systems:

    * Fedora 20 though 23
    * FreeBSD 9.1-RELEASE
    * FreeBSD 10.1-RELEASE
    * Linux Mint 13
    * OpenSUSE Tumbleweed (2016*)
    * Ubuntu 12.04
    * Ubuntu 14.04
    * Ubuntu 16.04

4\. Install with `sudo make install` or use Checkinstall to produce an uninstallable package with `sudo checkinstall`. (In the former case you can uninstall s2png with `sudo make uninstall`.)

### Windows

You will need [MSYS2](http://msys2.github.io/). Install it and start the MSYS2 MINGW32 Shell.

1\. Install the build dependencies.

```sh
pacman -Syuu diffutils git make mingw-w64-i686-gcc mingw-w64-i686-gd mingw-w64-i686-imagemagick wget
```

2\. Clone the repository and `cd` into it.

```sh
git clone https://github.com/dbohdan/s2png
cd s2png/
```

3\. Get `sysexits.h`, which is required to build s2png, and modifty `s2png.c` to use it.

```sh
wget https://raw.githubusercontent.com/freebsd/freebsd/master/include/sysexits.h
sed -i 's/<sysexits.h>/"sysexits.h"/' s2png.c
```

4\. Build `s2png.exe` executable with `make`.

5\. Create a new directory. Copy the binary and its DLL dependencies there.

```sh
mkdir build/
cp s2png.exe build/
cp /mingw32/bin/{libbz2-1.dll,libexpat-1.dll,libfontconfig-1.dll,libfreetype-6.dll,libgcc_s_dw2-1.dll,libgd-3.dll,libglib-2.0-0.dll,libgraphite2.dll,libharfbuzz-0.dll,libiconv-2.dll,libintl-8.dll,libjpeg-8.dll,liblzma-5.dll,libpcre-1.dll,libpng16-16.dll,libstdc++-6.dll,libtiff-5.dll,libvpx-1.dll,libwinpthread-1.dll,libXpm-noX4.dll,zlib1.dll} build/
```

The contents of `build/` will run on Windows machines without MSYS2.

Usage
-----

    s2png ("stuff to png") version 0.7.1
    usage: s2png [-h] [-o filename] [-w width (600) | -s] [-b text]
                 [-p password] [-e | -d] file
    
    Store any data in a PNG image.
    This version can encode files of up to 16777215 bytes.
    
      -h            display this message and quit
      -o filename   output the converted data (image or binary) to filename
      -w width      set the width of the PNG image output (600 by default)
      -s            make the output image roughly square
      -b text       custom banner text ("" for no banner)
      -p password   encrypt/decrypt the output with password using RC4
                    (Warning: do not use this if you want actual secrecy!)
    Normally s2png detects which operation to perform by file type. You can
    override this behavior with the following switches:
      -e            force encoding mode
      -d            force decoding mode

Examples
--------

To store foo.mp3 in an image enter the following on the command line:

    s2png foo.mp3

A file named foo.mp3.png will be created in the same directory as foo.mp3.

Add the `-s` switch to ensure the resulting image is, give or take a pixel, square and `-b "some text"` to change the text of the banner at the bottom.

    s2png -s -b hello foo.mp3

To decode decode_me.mp3.png and get the original file decode_me.mp3 run the command

    s2png decode_me.mp3.png

If you got decode_me_v2.mp3.png as random_letters.png you could decode it directly to decode_me_v2.mp3 with

    s2png -o decode_me_v2.mp3 random_letters.png
