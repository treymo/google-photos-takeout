# Google Takeout Helper

## Install
1. Make sure Python 3 is installed as well as `pip` for python 3
1. Install ImageMagick version 7 with HEIC support.
  * uninstall default libhefi (if it's older than 1.51.  If it's >= 1.5.1 you can skip building and installing libheif)
  * build and install [libheif-1.5.1)[https://github.com/ImageMagick/libheif) manually from source. This was required for
    me on Ubuntu to build ImageMagick 7 correctly with HEIC support.
  * `sudo apt install build-essentials libheif-dev`
  * Download source for ImageMagick 7
  * Uncomment all 'build-deps's in `/etc/apt/sources.list`
  * `apt-get build-dep imagemagick`
  * `./configure --with-heic`
  * `make`
  * `sudo make install`
  * `sudo ldconfig /usr/local/lib`
1. Install `libmagickwand-dev`?
1. Install Wand: `pip install Wand`

## Recover your photos from Google Photos

1. Download all `.zip` archives for
   [*only* Google Photos data](https://takeout.google.com/settings/takeout).
   For me, selecting more than Google Photos resulted in an error. This is most
   likely because of the size of **all** of my Google data being so massive.
    *  Note: It can take hours or even days for Google to generate Zip files with
       all your data.
1. Run `./organize.py <directory where all your archives are>`.  For example:
   `./organize.py --photos_dir ~/Downloads/google_takeout_archives/`.  The
   script will:
    *  Find all of the takeout archives in this directory
    *  Extract the photos from these archives
    *  Delete extra metadata files (i.e. not the images and videos)
    *  Give you an option to delete the archives after to reclaim some hard
       drive space.
1. (Strongly recommended) Back up your photos somewhere else.  Google does a ton
   of work to make sure your images will never be accidentally deleted or lost.
   It's very unlikely you are willing/able/can afford to have the same
   level of reliability as Google.  I'm no expert, but I've found [this subreddit's
   wiki](https://www.reddit.com/r/DataHoarder/wiki/backups) to be a good
   starting point for learning about how to back up.

## Extract all attachments from the mail archive

1.  Download the `.mbox` archive with Gmail data
2.  Run `./organize.py --mbox_file <path to .mbox file>`
