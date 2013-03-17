s2png — "something to png"
==========================

This program converts binary files of any kind into new PNG images and vice versa. It was originally developed by k0wax at http://sf.net/projects/s2png/. This fork fixes the problem that causes the s2png to segfault when compiled on modern GNU/Linux distributions.

Building
--------

1. Install the dependecies. In Debian, Ubuntu and Linux Mint you can do so with
  
    sudo apt-get install libgd2-xpm-dev libgd2-xpm

2. Type "make" in your terminal and hit the enter key.

Building has been tested in Linux Mint 13 and Ubuntu 12.10.

Installing
----------

    sudo make install
    
On Debian your should instead use

    sudo checkinstall

Usage
-----

    usage: s2png [-h] [-o filename] [-w width (600)] file 
        
      -h            display this message and quit
      -o filename   output the coverted data (image or binary) to filename
      -w            set the width of PNG image output (600 by default)

Basic examples
--------------

    $ s2png 1.mp3
   
Now you have 1.mp3.png in the same directory as 1.mp3.

Suppose you need decode file DecodeMe.mp3.png. Type

    $ s2png DecodeMe.mp3.png

Now you have the original DecodeMe.mp3 in the same directory as DecodeMe.mp3.png.

