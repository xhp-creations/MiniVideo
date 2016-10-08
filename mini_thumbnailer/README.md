mini_thumbnailer
================

Introduction
------------

mini_thumbnailer is a thumbnail picture extraction software.


Building mini_thumbnailer
-------------------------

Do not forget "FindLibMiniVideo.cmake" directory in the cmake/modules/, which defines
how to find the library (libminivideoframework.so file) and its header (minivideoframework.h file)
In case of problem, it may be necessary to manually indicate the paths of these files.

minivideo library must have been built first.

> $ cd mini_thumbnailer/build/  
> $ cmake ..  
> $ make  

Installation into the system, available for root user with both testing softwares:
>  $ su  
>  # make install # INSTALLATION INTO THE SYSTEM, ROOT USER ONLY  


Using mini_thumbnailer
----------------------

> $ cd mini_thumbnailer/build/  
> $ ./mini_thumbnailer -i 'myfilepath' [-o 'mydirectory'] [-f picture_format] [-q picture_quality] [-n picture_number] [-m picture_extractionmode]  

Command line arguments:
> -h : print help  
> -i : path to the input video  
> -o : path to the output folder, where generated thumbnails will be saved  
> -f : export format for the thumbnails (can be 'jpg' 'png' 'bmp' 'tga' 'yuv420' 'yuv444')  
> -q : thumbnail quality (1 to 100 range)  
> -n : number of thumbnail to generate (1 to 999 range)  
> -m : extraction mode for the thumbnails (can be 'unfiltered', 'ordered' or 'distributed')  