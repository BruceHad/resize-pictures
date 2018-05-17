Resize Images
=============

2017-01-24

Very basic bash script I use to resize batched of photographs.

To Do:

- [x] Rename files based on date.
- [ ] Fix empty folder issue
- [x] Append text to resized image (e.g. *_small_.jpg)
- [ ] Recursively search folders.
- [ ] Error handling
- [ ] Maybe put an absolute sizing option, rather than a percent???

Requirements
------------

Should run on a linux system with ImageMagick installed.

'convert' is a command line tool from the ImageMagick. To install

    sudo apt-get install imagemagick

Usage
-----

To run:

    ./resize source_path destination_path reduce_percent append

* The source path is the folder containing all the files. 
* The destination_path is where you want the file placed. reduce_percent is the % value to be passed to convert e.g. '50%'
* The append value will be appended to the filename after resize. e.g. *_small.jpg*

The script will check the source directory for all .jpg files. Each jpg will be converted and resized, then copied to the destination directory.

Then it will search through any subfolders and repeat. The folder names will be retained in the destination directory.

Notes
-----

### ImageMagick

* http://forums.fedoraforum.org/showthread.php?t=242084
* http://ask.xmodulo.com/install-imagemagick-linux.html

The basic command to reduce an image size by 50% is:

    convert image.jpg -resize 50% image_new.jpg
    
To do a bulk update of all files in a directory:

    for i in *.jpg; 
        do convert "$i" -resize 50% "${i%%-jpg*}_new.jpg"; 
    done

And to recursivelly update all images in multiple subfolders:

     find . -type f -name "*.jpg" | while read i; do convert "$i" -resize 50% "${i%%.jpg*}_new.jpg"; done 

### Bash Scripts in Linux

* https://www.linux.com/learn/writing-simple-bash-script

The first part of the script is called the shebang, which includes the path to the shell the script uses.

    #!/bin/bash

File must be executable so change it:

    chmod 700 script
    
To run the script, cd to the directory and:

    ./script

### Variables

Variables can be set and then used (with the $ sign).

    SOURCE=/home/user/Documents/
    echo $SOURCE

### Arguments

You can also take arguments from the command line.

    echo $1

    >> script foo
    foo