
[Click to access the associated YouTube video for this lesson](https://www.youtube.com/watch?v=p8VQmk_zbVo&list=PLmPit9IIdzwQl1kuuoEhG38DC3cdbqZHB&index=4&ab_channel=CloudWithVarJosh)

# File Types in Linux

> You would often hear people say Everything in Linux is a file. We will understand the reason for the same in the following text.

There are broadly 3 types of files:

 1. **Regular or Ordinary files:** like `file1` and `file2` that we saw in the previous lesson. Any binaries, video files, text files, images, tar files, CSVs, compressed files, etc. fall under this category.
You can use the `file` command or `ls -l` to identify the type of a file. The first character in the output, which is `-` for regular files, tells the type of a file when you use `ls -l`.
![Alt text](/images/4-file-1.png)

 3. **Directories:** These are files that help create a hierarchy. Directories are also files. but instead of storing data, they store the location of other files.
 ![Alt text](/images/4-file-2.png)

 4. **Special Files:** Linux treats all hardware devices (such as hard drives, SSDs, printers, monitors, floppy drives terminal emulators, and CD/DVD drives) as special files. 

Special files can be further categorized into 5 types:

 - **Linux Character files:** These are denoted by the letter **c**. A char file is a hardware file that reads/writes data in a character-by-character fashion. Some examples are a keyboard, mouse, and serial printer.
 
We will discuss the pipe `|` and `grep` in greater detail in later lessons. But I will give you a gist of these; The pipe symbol is used to send the output `STDOUT` of 1 command as input `STDIN` to the second command. `grep` utility or command is used to filter the required from the output or a file.

The command you see in the below snip says, do `ls -l` in the `/dev` directory, whatever output you get filter or grep the lines where the first character is the letter **c**. The first character is achieved by using the caret `^` symbol. From the output you get now show me the first line only. This is the reason you only see 1 line. Try to run `ls -l` on the `/dev` directory and see how lengthy the output is.
You would often see admins using `grep` and `|` in conjunction.
![Alt text](/images/4-file-3.png)

 - **Block files:** These are denoted by the letter **b**. A block file is a hardware file that reads/writes data in blocks instead of character by character. This type of file is very useful when we want to read/write data in bulk fashion. All our disks such are HDDs, SSDs, USBs, and CDROMs are block devices.
 ![Alt text](/images/4-file-4.png)
 - **Link files:** These are denoted by the letter l. These depict hard and symbolic links.
 ![Alt text](/images/4-file-5.png)
 - **Named pipes:** These are denoted by the letter **p**. It is a file used by two processes to communicate with each other and acts as a Linux pipe. It operates as a bidirectional communication channel, where one process writes data to the pipe, and another process reads it. It enables communication between processes without the need for shared memory or explicit socket connections.
![Alt text](/images/4-file-6.png)
- **Linux socket files:** These are denoted by the letter s. Let's first understand what a socket is in general, forget Linux for a while. A socket passes data between 2 processes. If Process-A in System-1 wants to speak to Process-B in System-2, it connects to the socket of Process-B in System-2. A socket has an IP address and a port number using which a client can connect to a server.

Coming to Linux Socket files, When it comes to intra-server communication i.e. local communication, Linux uses socket files. Socket files allow applications of the local system to exchange data without going through the complex process of networking and sockets.
Hence, Socket files are the special files that use a file name as their address instead of an IP address and port number. 
Sockets provide a mechanism for processes to exchange data, similar to named pipes or network sockets.
![Alt text](/images/4-file-7.png)

# Linux Directory Structure
At the top, there is the root directory.

![Alt text](/images/4-file-8.png)

`/root`: Home directory of the superuser root.
`/boot`: Contains files required to boot the system.
`/etc`: directory contains all the system-wide configuration files. Basically, every single kind of configuration file is located in /etc, including but not limited to system configuration files
`/mnt`: This directory is used for mounting temporary file systems.
`/proc`: The “files” it contains are peepholes into the kernel itself. The files are readable and will give you a picture of how the kernel sees your computer.
`/sys`: Contains information about devices, drivers, and some kernel features.
`/dev`: Linux places all special files, remember we saw this file type a while ago, under the `/dev` directory.
`/home`: In normal configurations, each user is given a directory in /home. A user has full permissions in its home directory. Like home directory of ec2-user is `/home/ec2-user`.

`/usr`: Acronym for *User System Resources*. `/usr` usually contains by far the largest share of data on a system. This directory contains most commands and executable files, libraries, and documentation. `/usr` is a place for system-wide, read-only files. So all your installed software goes here.
`/usr/bin`: contains non-essential binaries.
`/usr/sbin`: similar to `/usr/bin`, but binaries here are intended to be used by the superuser root. Whenever you see `/sbin` or `/usr/sbin` think superuser.
`/bin`: contains essential binaries that are required by the system for emergency repairs, booting, and single-user mode. For this reason and in contrast to `/usr/bin`, the binaries in this directory are considered to be essential. Examples include `ls`, `cat`, `cp` (which is used to copy files). 
`/sbin`: similar to `/bin`, but the binaries present here are intended to be used by the superuser root.

`/lib`: lib is short for *library*. Keeping Linux aside. A library in programming is a collection of prewritten code that programmers can use to optimize tasks.  The library is a component that the main program needs to run properly. If a binary or executable in `/bin` or `/sbin` needs a library that library is likely in `/lib`.
You would see people use different terminologies, but for all intent and purposes: binaries, executables, and programs imply the same.
`/var`: This directory contains system logs and other various variable data.
