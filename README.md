MiniVideo
=========


Introduction
------------

MiniVideo is a small video decoding library developed from scratch in C, bundled with small testing programs developed in C++.  
MiniVideo has been tested with several CPU architectures (x86, SH4, mips, arm).  
The build system uses CMake. Both library and test programs can be installed into your system.  

MiniVideo has been developed in 2010-2011 during an internship I did in the company "httv". Its goal is to provide a source code that is easy to read and to understand, destined for learning purpose. After a clean-up pass, the code has been published early 2014 with httv permission under the LGPL v3 license (decoding backend) and GPLv3 (testing softwares).  

The minivideo library can:
* Open video files with various container to demux and remux audios/videos contents.
* Open H.264 video stream and decode them to export intra-coded pictures.

### Supported video codec (decode)
- H.264 / MPEG-4 part 10 "Advance Video Coding"

### Supported container formats (import module)
- Elementary stream H.264 ("Annex B" format) [.264]
- Elementary stream MPEG-1/2 [.mpg, .mpeg]
- PS (MPEG Program Stream) [.mpg, .vob, ...]
- MP4 (MPEG ISO container) [.mp4, .mov, .3gp, ...]
* MKV (Matroska, Work In Progress) [.mkv, .webm]
* AVI (Work In Progress) [.avi]

### Supported picture formats (export module)
- bmp
- tga
- tiff
- png (with external libpng support)
- jpeg (with external libjpeg support)


Generate online documentation with Doxygen
------------------------------------------

$ cd minivideo/doc/
$ ./generate_doxygen.sh

Open "minivideo/doc/doxygen.html" with your favorite browser.


Generate error report with cppcheck
-----------------------------------

$ cd minivideo/doc/
$ ./generate_cppcheck.sh

Open "minivideo/doc/cppcheck.html" with your favorite browser.


To build the minivideo library:
-------------------------------

$ cd minivideo/build/
$ cmake ..
$ make

$ su
# make install // INSTALLATION INTO THE SYSTEM, ROOT USER ONLY

### cmake parameters:
-DCMAKE_BUILD_TYPE=Release/Debug
-DCMAKE_BUILD_Mode=Dynamic/Static
-DCMAKE_TOOLCHAIN_FILE=../cmake/toolchains/xxx.cmake
-DCMAKE_INSTALL_PREFIX=/usr/bin

You can also change several build options into the "minivideo/CMakeLists.txt" file.


To build the minivideo testing softwares:
-----------------------------------------

Do not forget "FindLibMiniVideo.cmake" directory in the cmake/modules/, which defines
how to find the library (libminivideoframework.so file) and its header (minivideoframework.h file)
In case of problem, it may be necessary to manualy indicate the paths of these files.

$ cd mini_extractor/build/
$ cmake ..
$ make

$ cd mini_thumbnailer/build/
$ cmake ..
$ make

$ su
# make install // INSTALLATION INTO THE SYSTEM, ROOT USER ONLY


mini_extractor usage:
---------------------

$ cd mini_extractor/build/
$ ./mini_extractor -i 'myfilepath' [-o 'mydirectory'] [-a nb_tracks] [-v nb_tracks]

Arguments:
-h : print help
-i : path to the input video
-o : path to the output folder, where extracted streams will be saved
-a : maximum number of audio stream(s) to extract
-v : maximum number of video stream(s) to extract


mini_thumbnailer usage:
-----------------------

$ cd mini_thumbnailer/build/
$ ./mini_thumbnailer -i 'myfilepath' [-o 'mydirectory'] [-f picture_format] [-q picture_quality] [-n picture_number] [-m picture_extractionmode]

Arguments:
-h : print help
-i : path to the input video
-o : path to the output folder, where generated thumbnails will be saved
-f : export format for the thumbnails (can be 'jpg' 'png' 'bmp' 'tga' 'yuv420' 'yuv444')
-q : thumbnail quality (1 to 100 range)
-n : number of thumbnail to generate (1 to 999 range)
-m : extraction mode for the thumbnails (can be 'unfiltered', 'ordered' or 'distributed')


MiniVideo decoding capabilities
===============================

Unsupported features regarding H.264 specification
--------------------------------------------------

// UNSUPPORTED for BP and XP profiles
(FMO) Flexible Macroblock Ordering
(ASO) Arbitrary slice ordering
(RS) Redondant slice

// UNSUPPORTED for XP profile
Data partitioning
SI and SP slices

// UNSUPPORTED for HiP profile (HIGH)
Major bug inside CABAC decoding process
Deblocking filter!!!
Interlaced coding (PicAFF, MBAFF)
4:0:0 "greyscale" subsampling

// UNSUPPORTED for Hi10P profile (HIGH + 10bits samples)
Sample depths > 8 bits

// UNSUPPORTED for Hi422P profile (HIGH + 10bits samples + 4:2:2 subsampling)
Sample depths > 8 bits
4:2:2 subsampling

// UNSUPPORTED for Hi444P profile (HIGH + 14bits samples + 4:4:4 subsampling)
4:4:4 subsampling
Separate color plane coding
Sample depths > 10 bits
IPCM macroblocks
