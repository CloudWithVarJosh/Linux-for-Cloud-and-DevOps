[Click to access the associated YouTube video for this lesson](https://www.youtube.com/watch?v=OGDEBvVqWeE&list=PLmPit9IIdzwQl1kuuoEhG38DC3cdbqZHB&index=2&ab_channel=CloudWithVarJosh)

# Navigation


Everything falls under the root of the file system. Root is depicted by a forward slash `/`. You would often hear people call this the root directory. 

> I have seen people getting confused between forward (/) and backward (\)
> slash. This may sound trivial but when the **top part** of a slash bends
> forward it is called a forward slash `/`.

The root directory happens to be the first directory in the file system, hence every other directory or file falls under the root directory.

The file system can be thought of as an upside-down tree where root is at the top and then there are branches to it. Branches are other directories and files.

Below is a graphical representation of an upside-down tree, what you see under the root are directories which could further have files and directories. In upcoming lessons, we will discuss the purpose of each directory that you see in the snip.

![Alt text](/images/fs.png)

# Absolute and Relative Path


## Absolute Path

> Refer to the snip `Absolute and Relative Path` while reading this section.

Think of it as an exact or complete path, hence it always begins from the root `/` because, as we discussed at the beginning, everything falls under the root.

I'm currently in the home directory of the `ec2-user`, we can check that by using `pwd`. If I want to go to `/usr/share/doc` then I use `cd /usr/share/doc`, since the path I used **begins with `/`** it is called an absolute path.

If you wish to go back to the previous working directory, which in our case is the home directory of the `ec2-user`, you can use the shortcut `cd -`.

![Absolute and Relative Path](/images/absolute.png)


## Relative Path
> Refer to the snip `Absolute and Relative Path` while reading this section.

Think of it as a shortcut. Relative path starts from the current working directory i.e. where you are in file system tree. Let's visit `/usr/share/doc` again. If I type `pwd` I can see I'm in the `doc` directory. You also see the current working directory listed in the prompt like we discussed in our previous lesson.

The parent directory for `doc` is `share` and the parent directory for `share` is `usr`. The shortcut to move to the parent directory is `cd ..` which will take you 1-step back in the file system.

If I wish to go to the `doc` directory again I can either use `cd /usr/share/doc` or I could just use `cd doc`. Using `cd doc` would be the relative path as it **starts from the current working directory**.

Let's again come 1-step back by using `cd..`, let's see where we are right now by using `pwd`. We're again in `/usr/share/`. In general speaking, you omit forward slashes and just say `usr share`.

You would also see SREs or admins using `cd ./doc` which also implies the same thing as `cd doc`. This is because `.` in Linux means the current working directory.

`cd ~` which will take you to the logged-in user's home directory which is `/home/ec2-user` in our case.
So, let's type `cd ~` and then use `pwd` to check where we are.

![Absolute and Relative Path](/images/absolute.png)

> Now that we understand the absolute and relative path, often a question
> comes to mind, should I use relative or absolute path?
> 
> Whichever you find easy. My bet is you found the relative path easier.
> Just note, as a best practice you should use absolute paths in **shell
> or bash scripting.**
## `/` vs `/root`
We haven't discussed home directory in detail, but for now, understand that every user has a home directory that can be found in `/home/<name-of-the-user>`. If I take the example of `ec2-user` its home directory is `/home/ec2-user`

Similarly, the superuser `root` also has a home directory which is `/root` (note it is not under `/home`). I want you to understand the difference between just a `/` and `/root`. The / is the root of the FS or root directory under which everything resides and then there is `/root` which is the home directory of the superuser `root`, which has unrestricted access to the Linux file system.

![/ vs /root](/images/fs2.png)
