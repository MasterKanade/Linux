What is a file?

1. A container for storing, accessing or managing data
2. Typically associated with a unique identifier or filename
3. This name is combined with its path, provides a unique location for each file in a file system.

File can have various attributes (stroed in inode):

1. Size: The amount of data stored in the file.
2. Permission: Who can read, write or execute the file.
3. Ownership: Which user or groups owns the file.
4. Timestamp: When the file was created, last accessed or modified.

How is the data stored?
==>
![how_data_is_stored](../images/how_data_is_stored.PNG)

How does folder work?
==>
![how_folder_work](../images/how_folder_works.PNG)

Files on Linux system:

1. In Linux and Unix like systems, (almost) everything is considered as a file.
2. This is part of unix philosophy.

For example:

1. Ordinary file (-)
2. Directories (d)
3. Symbolic links (l)
4. Character device (c)
5. Block device (b)
6. Named pipes (p)
7. Sockets (s)

We can show the type of the file with ls command

1. ls -l [folder_name / file_name]
2. Then the type will show the first character of the first column.

-rw-rw-r-- 1 mayur mayur 9019 Apr 12 11:46 document.txt

Here, - in the above line will shows up that this is a file type.

---

What is Symlink?
==>

1. A symlink is a special kind of file on Unix Systems
   Purpose:
   A. It serves as a reference to another file or directory.
   B. It is a special way of "shortcut" to another destination.

The idea:

1. We create a special file, that contains a reference to the destination path.
2. This reference is being resolved on access of the symlink (or a file within it)
3. This affects the read and write operations

How to create a symlink?
==>

1. we can use ln -s command for this
2. ln is a tool to make a links between files
3. we can use it to create symlink
   Syntax:
   ln -s target link
   Example:
   ln -s ~/Desktop deskshortcut

To verify:
ls -l
then if the first character is l then this file is a symlink.
lrwrwxrwx

ls -l deskshortcut
lrwxrwxrwx 1 mayur mayur 8 May 15 11:00 deskshortcut -> Desktop/

===

What is Hardlink?
==>

1. A hardlink is a directory entry or reference to an existing inode
2. Technically, first filename of a file is already a hardlink
3. But one file can have multiple hardlinks
   Thus:
   Hardlink beahve as if they were the same file
   A hardlink can only link to files on the same filesystem
   The filesystem must support additional hardlinks

If we delete hardlink:

1. The other filenames/hardlinks remain same intact
2. The data is only deleted if all hardlinks are removed.

![hardlink](../images/hardlink.png)

How can we create a hardlink?
==> we can use ln command for this (without -s option)
Syntax:
ln target hardlink

example:
ln ~/Desktop deskshardlinked

Limitation of hardlink is : we can not create hardlink on the directories (to prevent loops)

if we change any of the file or update any of the file then original file also get changed automatically, this is the way we can achieve hardlink in the linux.

Copy whole folder structure with hardlinks:
=>

1. cp -al source destination
2. This will copy the whole source folder, and create hard links for all files
3. We will not need any additional storage for this
4. We can now organize the files in multiple different folder structures, without needing any additional disk space

===

Troubleshooting the Inode limit:

Increasing the Inode limit:

1. During the creation of a filesystem, space is reserved for inodes. (at centralized location)
2. This space can't be used for anything else
3. We can show how many inodes are being used:
   df -ih

Usually the limit should be sufficiently high, so we'll never reach it.

But if your application uses many small files then

1. this can be therotically reached
2. Processes or applications crash or can't be started
3. Operating system crashes

to solve this:

1. You can remove files that are no longer needed.
2. You can compress many files into an archieve (for example .tar)
3. You can recreate your inode filesystem with a higher inode limit.
4. You can store data on additional drives (and mount them)

===

Buffered v/s UnBuffered I/O

1. Unbuffered Input/Output
   a. Directly handles data between the I/O device and the program
   b. Real time data: we get immediate access to the data
   c. Control: offers more precise control over data flow and timing
   Examples: Reading data from keyboard, Reading data from sensors.

check with following command to take input from the Mouse:
sudo cat /dev/input/mice

2. Buffered Input/Output:
   a. Utilizes temporary storage area (buffer) to hold data before it's being received/sent to the I/O device.
   b. Advantages:
   Efficiency: Reduces the number of I/O operations by accumulating data before processing.
   Performance: Enhances speed, especially for disk and network operations.
   Data Integrity: Simplifies the implementation of data integrity checks.
   Ideal for large, sequential data transfers.

Typical examples:

1. Reading file from the disk
2. Writing data to disk in blocks.

===

What is a device?
==>

1. A device refers to a physical or virtual entity that can be accessed through a file-like interface.
2. Device in unix serve as the interface between the operating system and various hardware or virtual components.
3. They allow applications and users to interact with these components by reading from and writing to their corresponding device files.
