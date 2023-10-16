
[Click to access the associated YouTube video for this lesson](https://www.youtube.com/watch?v=JAzwS38hCA8&list=PLmPit9IIdzwQl1kuuoEhG38DC3cdbqZHB&index=3&ab_channel=CloudWithVarJosh)

# ls command


`ls` is used to list the contents of a directory. If I hit ls I see file1, file2, directory1, and directory2. If you are following along you can type `touch file1 file2` to create file1 and file2, and use `mkdir directory1 directory2` to create directory1 and directory2. 
>In summary, `touch` can be used to create files and `mkdir` to create directories.

We can use `ls directory1` to see the contents of directory1. To see the contents of multiple directories at once you can use `ls directory1 directory2`.

Remember we discussed `~` represents the home directory of the logged-in user. You can use `ls ~` to list the contents of the logged-in user's home directory.

![Alt text](/images/3-ls-1.png)



The output we have seen thus far is precise, if we want a long format output we can use `ls -l`. `-l` is an option that can be used with the ls command. 
>Options allow us to modify the behavior of a command. And they are case-sensitive.

There are a plethora of options that we can use with ls. We can use `ls --help` to see all of them.

Options are of 2 types:

 1. Short
 2. Long

**Short** options are preceded by a single `-` and many commands allow multiple short options to be strung together.
**Long** options are preceded by double `--` hyphens.

The format of the command looks like this: `command -options argument`
For e.g. `ls -l directory1` 

> Don't be shy of using `--help`, as an experiment try to use it with the
> commands you have learned in past lectures. You are learning Linux
> now, and soon you will start working with Docker, Kubernetes, Helm,
> and many more tools, and most of them will have a `--help` feature. This
> will be your guiding force throughout your **DevOps** and **Cloud** journey.

## Understanding `ls -lthr` output

A few of the flags that you'll use all the time with `ls` are `-lthr`
`l` stands for long listing
`t` stands for sort by modification time, and newest first.
`h` stands for, you guessed it right, to make the file or directory size human-readable.
`r` stands for reverse order while sorting
And you can read about the rest of the available options using `ls --help`

![Alt text](/images/3-ls-2.png)

The following snip explains the output of the command:
![Alt text](/images/3-ls-3.png)

We will discuss file types and permissions in later lessons, but I want to give you a one-line about **`-rw-rw-r--`** which constitutes 10 characters. The first character denotes the file type and the remaining 9 character represents the file permissions.

- The first `-` signifies it is a file, a directory will have a `d` here like directory1 has it.
- The first triplet i.e. `rw-`, shows the permissions of the owner on the file
- The second triplet i.e. `rw-` shows the permissions of the group on the file. The group will have members. Most Linux distros will create a group with the same name as the user and add that user to that group, here you can see a group with the name ec2-user created. 
- The third and the final triplet show the permission for everyone else (or others) on file2.

Just so you know r stands for read, w stands for write and the 3rd character is for execute, which you see is missing in all the 3 triplets, but it is there in directory1.


# Hard and Symbolic Links
## Hard Links
Every file on the Linux file system starts with a **single** hard link. This link is between the filename and the actual data stored on the file system.
For eg. If I create a file with the name `file1` and write `foo` in `file1` then the link between `file1` and the data stored in the file is called a hard link. I can verify the number of hard links a file has by typing `ls -l`. You see the numerical 1, it depicts this file has 1 hard link.

![Alt text](/images/3-ls-4.png)

We can use the cat command to see the contents of a file. cat file1 shows me the contents of file1.
The syntax for creating hard links is `ln <original file path> <new file path>`

So let us create a hard link to `file1`: I will type `ln ~/file1 /tmp/file1_hl`. Here I'm creating the hard link to `file1` in the `tmp` directory.

![Alt text](/images/3-ls-5.png)

If I do `ls -l file1` I see this file now has 2 hard links. The 1st was automatically created when the file1 was first created and the 2nd one we just created. Similarly, if I do `ls -l /tmp/file1_hl` I see 2 hard links. 
Here we know `file1` and `file1_hl` are hard-linked, but if you find two files with identical properties but are unsure if they are hard-linked, use the `ls -i` command to view the inode number. 

> Files that are hard-linked together share the same inode number.

![Alt text](/images/3-ls-6.png)

**What is an inode?**
Every file in Linux gets an inode. Inodes in Linux stores metadata for every file on your system. Metadata like the location of the file on the disk, permissions, size, owner/group info. and much more. They store all the information except the file name and the actual data.

Hard links essentially point to the same inode number. We can check the inode number using `ls -i.`
`ls -li file1 /tmp/file1_hl` gives me a long listing because I used the -l option and also the inode because I used the `-i` option. You see I just **chained 2 short options** together. 
What we see in the output is, we have the same inode no., which implies they have the same data. 

![Alt text](/images/3-ls-7.png)

Since they point to the same inode, if I change content of `file1`, then `file1_hl` will also show the changed content. Let's add another line to `file1`: `echo "bar" >> file1`.
I will `cat file1` now and I see `foo bar`. Now let's `cat /tmp/file1_hl` and I see the same content.

![Alt text](/images/3-ls-8.png)

`echo` is used to enter text in a file or output text. When used with `>` it overwrites the existing text in the file and with `>>` it appends the supplied text in the file. I will elaborate on these in later lessons. 

I want you to understand that you can create many hard links to a file and they will have the same inode. The inode is only deleted when **all** the hard links are deleted.

> Note: Hard links are only valid within the same File System. Symbolic
> links on the other hand can span file systems as they are simply the
> name of another file.


## Symbolic Links (aka Symlinks)
Symlinks are like shortcuts in Windows OS. If the original file is deleted then the shortcut is of no use. Similarly, if a file to which a symlink points to is deleted then the symlink is of no use. This situation is known as the dangling symlink or a broken symlink. If you recreate the file to which the symlink was pointing to the symlink starts functioning again.

The syntax of creating symlink is `ln -s <original file path> < new file path>`. Syntax is similar to hard link, you just have `-s` extra.
Let's create `file2` and put some content in it. I'll add `foo bar` to it. I will now create a symlink by typing `ln -s ~/file2 /tmp/file2_sl`. I'll now check the inode for `file2` and its soft link.
`ls -li file2 /tmp/file2_sl`. You see the inodes are different, this is the reason the symlink is of no use when the original file is removed, as the symbolic link points to the original file whereas hard links point to the actual data, not the filename.
![Alt text](/images/3-ls-9.png)

The following snip shows a situation when the original file to which the symlink points to is deleted.

![Alt text](/images/3-ls-10.png)

`rm` command is used to remove files.
`file` command helps determine the type of a file and its data.


> You would often hear symbolic links referred to as **soft** links. Refrain
> from calling them soft links as the Linux community doesn't like this
> term.
