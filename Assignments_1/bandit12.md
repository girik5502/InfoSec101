# Bandit Level x to y Writeup


Author: [Girik Maskara](https://github.com/girik5502) 

Problem Page: [bandit12](https://overthewire.org/bandit/bandit12) (Change this link accordingly)

## List of Commands Used
```
ls - list files in a directory
mkdir - make a new directory
cp - copy a file or directory to desired location
cd - move to another directory
xxd - make a hexdum of a file 
xxd -r - reverse hexdump
mv - rename a file
gzip - compress or expands a file
gzip -d - decompress the file
bzip2 - block-sorting file compressor
bzip2 -d - decompress the file
tar - an archiving utility
cat - read the contents of a file
file - returns the type of a file
```

## Walkthrough
How did you solve this level? Include the complete thought process, even stuff that didn't work. Give explanations wherever necessary.
The given file data.txt  has been repeatedly compressed and then further made into a hexdump. So to constantly decompress it, it will be useful to make a new folder as we will have to store a lot of temporary files. The first step is to get the actual compressed file from its hexdump, which is done by the xxd -d command. Then we do the decompression part. We first find the file name and type using ls and file commands. For the first case, it’s a gzip compressed file. So, I first tried using the gzip -d but later found out that I need to make a filename with .gz at the end which I made using mv.
Then repeated the above steps until I got a text file which contains the password (the file formats were gzip, bzip2 and tar for which I respectively used gzip -d,bzip -d, tar -xf).


## Password
8ZjyCRiBWFYkneahHwxCv3wb2a1ORpYL

## Bash/Python script to automate the process
```
ssh bandit12@bandit.labs.overthewire.org -p 2220 "mkdir /tmp/2000;
xxd -r data.txt > /tmp/2000/1;
cd /tmp/2000;
mv 1 1.gz;
gzip -d 1.gz;
mv 1 1.bz2;
bzip2 -d 1.bz2;
mv 1 1.gz;
gzip -d 1.gz;
mv 1 1.tar;
tar -xf 1.tar;
mv data5.bin 2.tar;
tar -xf 2.tar;
mv data6.bin 1.bz2;
bzip2 -d 1.bz2;
mv 1 1.tar;
tar -xf 1.tar;
mv data8.bin 1.gz;
gzip -d 1.gz;
cat 1"
```
