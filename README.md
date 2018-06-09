# cbmage 0.2
Print a picture from a modern PC with an old-fashioned **Commodore MPS 803** compatible printer
## Purpose
This utility outputs raw bytes for printing on a [Commodore MPS 803](http://www.zimmers.net/cbmpics/p6serial3.html) compatible printer. It should be used with [**opencbm**](http://spiro.trikaliotis.net/opencbm) package by [Spiro Trikaliotis](http://spiro.trikaliotis.net/) to redirect the output to the printer, connected through a [XUM1541 cable](https://rdist.root.org/2009/01/21/introducing-xum1541-the-fast-c64-floppy-usb-adapter/), such as [ZoomFloppy](http://www.go4retro.com/products/zoomfloppy/).

## Contents of package
- **source** - Source code in C
  - [**cbmage.c**](https://github.com/sblendorio/cbmage/blob/master/source/cbmage.c) - Main program
  - [**stb_image.h**](https://github.com/sblendorio/cbmage/blob/master/source/stb_image.h) - [STB library](https://github.com/nothings/stb) by [Sean Barrett](https://twitter.com/nothings) for reading image files
  - [**stb_image_resize.h**](https://github.com/sblendorio/cbmage/blob/master/source/stb_image_resize.h) - [STB library](https://github.com/nothings/stb) by [Sean Barrett](https://twitter.com/nothings) for resizing images
  - [**Makefile**](https://github.com/sblendorio/cbmage/blob/master/source/Makefile) - Makefile
- **binaries** - Precompiled executable files for different platforms
  - **win32**/[**cbmage.exe**](https://github.com/sblendorio/cbmage/blob/master/binaries/win32/cbmage.exe?raw=true) - for **Windows XP**
  - **win64**/[**cbmage.exe**](https://github.com/sblendorio/cbmage/blob/master/binaries/win64/cbmage.exe?raw=true) - for **Windows 10**
  - **macOS**/[**cbmage**](https://github.com/sblendorio/cbmage/blob/master/binaries/macOS/cbmage?raw=true) - for **macOS**, 64 bit
  - **linux64**/[**cbmage**](https://github.com/sblendorio/cbmage/blob/master/binaries/linux64/cbmage?raw=true) - for **Linux** (x86_64)

## Requirements
- **macOS** or **Windows** (32/64 bit) or **Linux**
- an **MPS 803** printer or a **compatible one**
- [**XUM1541**](https://rdist.root.org/2009/01/21/introducing-xum1541-the-fast-c64-floppy-usb-adapter/) / [**ZoomFloppy**](http://www.go4retro.com/products/zoomfloppy/)
- [**opencbm**](http://spiro.trikaliotis.net/opencbm) package installed (a.k.a. **cbm4win**)
- **gcc** if you want to compile from sources

## Install ***opencbm***
To install [**opencbm**](http://spiro.trikaliotis.net/opencbm) you can use the installer from its website, or if you use a debian-based version of Linux, you can install it with:

`sudo apt-get install opencbm`

on macOS you can use a similar command (with the help of [Homebrew Package Manager](https://brew.sh/)):

`brew install opencbm`

## Compiling ***cbmage***
Once you have **gcc** installed, enter the **"source"** directory and launch:

`make`

An executable file named **"cbmage"** will be generated: it's ready to use.

## Using ***cbmage***

Synopsis:

`cbmage <image file name>`

This is the basic syntax: it will write on *stdout* (i.e. the terminal window) the raw bytes that will be interpreted by the **MPS 803** printer. Quite useless if not redirected to a real printer.

## Let's use it with ***opencbm***

The typical sequence of commands you should use to do the task is the following:

    cbmctrl reset
    cbmctrl lock
    cbmctrl listen 4 0
    ./cbmage picture.png | cbmctrl write
    cbmctrl unlisten
    cbmctrl unlock

In particular, the **4th line** (`./cbmage picture.png | cbmctrl write`) produces the raw bytes (launch it **without "./"** if you run it **on Windows**), which are redirected to the printer through the piped `cbmctrl write` command.

## Restrictions
* **Maximum width** on a Commodore MPS 803 is **480 dots** per row. Therefore the image will be automatically resized to that width if it exceeds that size.
* The printer is a **black and white** one. The _recommended_ format is **PNG**: every single dot which is **white** (total white: `#ffffff` in hex) will be left blank, while **any** other pixel color will result in a **black** dot on the printer.

## Credits
Thanks to [**Spiro Trikaliotis**](http://spiro.trikaliotis.net/) for the [opencbm package](http://spiro.trikaliotis.net/opencbm), to [**Till Harbaum**](http://spiro.trikaliotis.net/xu1541) for the initial case study of the [XU1541](http://spiro.trikaliotis.net/xu1541) (and also for the fantastic [MIST](http://harbaum.org/till/mist/index.shtml)) and to [**Sean Barrett**](https://twitter.com/nothings) for his powerful and effective [STB Image Library](https://github.com/nothings/stb).

## Sample printed **PNG** files
![MPS 803 - 1](http://www.sblendorio.eu/images/mps803-1.jpg)
![MPS 803 - 2](http://www.sblendorio.eu/images/mps803-99.jpg)
![MPS 803 - 3](http://www.sblendorio.eu/images/mps803-3.jpg)
![MPS 803 - 4](http://www.sblendorio.eu/images/mps803-2.jpg)

