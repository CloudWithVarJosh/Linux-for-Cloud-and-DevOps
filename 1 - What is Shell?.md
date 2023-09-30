# What is shell?

- Shell takes commands and passes them to the Operating System (OS), it is an interface between you and the OS. When I say CLI (which is an acronym for command line interface), command line, it all refers to the shell.
- A popular shell program is bash. Bash is an acronym for **b**ourne-**a**gain **sh**ell.
- You see bash is an enhanced version of sh. And sh is the original shell program written by Stephen Bourne.

What you see at the bottom right is a shell prompt. Typically you would see username@hostname followed by the current working directory. At the end you see a dollar`$`, if you see a hash `#` instead of a Dollar `$` it implies you are logged in as a superuser (often root).
You can check the hostname of your machine by typing `hostname`.

In the picture below the user with which I have logged in is "ec2-user" and the hostname of the instance is ip-172-31-36-89. I'm working with an Amazon EC2 instance and that is the format in which AWS assigns hostnames when an instance is launched. There is another format called, *Resource name*, that AWS uses to assign hostnames but that is outside of what we are discussing right now.

![Alt text](/images/hostname.png)

The `~` you see at the end i.e. after 89 signifies I'm in the home directory of the ec2-user i.e. the user via which I've logged in. We will discuss more about `home directory` in later lessons.


## Few Basic Commands

- **hostnamectl**
`hostname` command we have already seen `hostnamectl` can be used to get a lot more information

![Alt text](/images/hostnamectl.png)


- **free**
 `free` gives us the memory statistics (total, used, and free memory). You can add `-h` to it to make it human-readable.

![Alt text](/images/free.png)

 
 - **cal**
 `cal` displays the calendar

![Alt text](/images/cal.png)

 
- **date**
 `date` displays today's date, based on your system's configuration.

![Alt text](/images/date.png)

 
- **df**
 `df` stands for *disk free*. It tells you the amount of free disk space.

![Alt text](/images/df.png)


- **history**
 A cool feature of the shell is command history. Most distros will remember the last 1000 commands by default. You can type `history` to see the previously executed commands.
 You can navigate through the command history using the up and down arrows, and press enter to execute the displayed command.
