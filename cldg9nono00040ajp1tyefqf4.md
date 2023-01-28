# This will help you get started with LINUX.

> Let's start with some basic queries you might have!

## Why Linux though?

* First of all, it's Opensource and hence there is a lot of customization that we can do.
    
* There is good community support.
    
* It supports a wide variety of hardware.
    
* Most servers are running on Linux.
    
* Automation is very easy to do on Linux.
    
* Linux is considered a secure operating system.
    

## Linux Architecture

![image.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1648450654404/TNZIZD4A_.png align="left")

## What are the basic Linux Principles?

* Everything is considered a file in Linux even the Hardware also the configuration files are stored in text files.
    
* Mostly we have small single-purpose programs and we have the ability to chain these programs together for complex operations.
    
* Try avoiding the Captive user interface.
    

![image.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1648451613299/nSeZc-MN6.png align="left")

## File Types

* Ordinary or regular files -&gt; Contain data of various content types such as text, script, image, videos, etc.
    
* Directory files -&gt; Contain the name and address of other files.
    
* Block or character special files -&gt; Represent device files such as hard drives, monitors, etc.
    
* Link files -&gt; Point or mirror other files
    
* Socket files -&gt; Provide inter-process communication
    
* Named pipe files -&gt; Allow processes to send data to other processes or receive data from other processes.
    

## Directory structure in Linux?

> Before checking on the Directory Structure, [Set Up your Linux Machine](https://carboncoffee.hashnode.dev/vagrant-part-1-greater-setting-vm-manually-vs-automatically)

* **Home Directories** -&gt; /root , /home , /username
    
* **User Executable** -&gt; /bin , /usr/bin , /usr/local/bin
    
* **System Executable** -&gt; /sbin , /usr/sbin , /usr/local/sbin
    
* **Other mountpoints** -&gt; /media , /mnt
    
* **Configuration** -&gt; /etc
    
* **Temporary files** -&gt; /tmp
    
* **Kernels** -&gt; /boot
    
* **Server data** -&gt; /var , /srv
    
* **System information** -&gt; /proc , /sys
    
* **Shared Libraries** -&gt; /lib , /usr/lib , /usr/local/lib
    

## Few basic commands that you wanna try before moving forward...

* **sudo** -&gt; this command enables you to perform tasks that require administrative or root permissions.
    
* \*\*cd \*\* -&gt; To navigate through the Linux files and directories
    
* **cd ..** -&gt; (with two dots) to move one directory up
    
* **cd** -&gt; to go straight to the home folder
    
* **cd-** -&gt; (with a hyphen) to move to your previous directory
    
* **ls** -&gt; to view the contents of a directory.
    
* **ls -R** -&gt; will list all the files in the sub-directories as well
    
* **ls -a** -&gt; will show the hidden files
    
* **ls -al** -&gt; will list the files and directories with detailed information.
    
* **cat &gt; filename** -&gt; this is used to creat a file also it can be used to join 2 files by giving the command - **cat filename1 filename2&gt;filename3**
    
* **cp** -&gt; this command is used to copy files from the current directory to a different directory.
    
* **mv** -&gt; this command is used to move files, although it can also be used to rename files.
    
* **mkdir &gt; directory\_name** -&gt; this command to make a new directory and **rmdir** is used to remove a directory.
    
* \*\* touch \*\* -&gt;this command allows you to create a blank new file through the Linux command line.
    

> There are much more available which you might want to check online but as of now we would be good.

## VIM Editor Linux

![image.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1648489244654/zn4mBA467.png align="left")

Vim is a highly configurable text editor built to make creating and changing any kind of text very efficient.

* Command to install VIM Editor
    

```plaintext
[vagrant@localhost ~]$ sudo yum install vim
```

* Once done, you might want to create a new file here. Use the below command and this should open a new file for you.
    

```plaintext
[vagrant@localhost ~]$ vim firstfile.txt
```

* There are 3 modes in VIM Editor.
    
* the first one is **Command Mode** -&gt; you are greeted with this mode
    
* the second one is **Insert Mode** -&gt; hit **'i'** to get edit insert/edit mode and hit **'esc'** to get back to command mode
    
* The third one is **Extended Command Mode** -&gt; give **':'** to get into this mode, you might want to give **':w'** to save the edited file, **':q'** to quit the file or **':wq'** to save and quit the file at the same time.
    
* Some of the frequently used commands are-
    
    * **x**\- to delete the unwanted character.
        
    * **u** - to undo the last command and U to undo the whole line.
        
    * **CTRL-R** to redo.
        
    * **A** - to append text at the end.
        
    * **:wq** - to save and exit.
        
    * **:q!** - to trash all changes.
        
    * **dw**\- move the cursor to the beginning of the word to delete that word.
        
    * **2w** - to move the cursor two words forward.
        
    * **3e** - to move the cursor to the end of the third word forward.
        
    * **0 (zero)** - to move to the start of the line.
        
    * **d2w** - which deletes 2 words .. number can be changed for deleting the number of consecutive words like d3w.
        
    * **dd** to delete the line and 2dd to delete to line .number can be changed for deleting the number of consecutive words.
        

## Filters

* Let's see a few commands related to filtering. The first one is the **grep** command, which will find a particular word across a file, lets's see if you want to find the word 'Firewall' in the file anaconda the command would be like.
    

```plaintext
[root@localhost ~]# grep Firewall anaconda-ks.cfg
```

* Since Linux is case sensitive we can use the following command to ignore the same.
    

```plaintext
[root@localhost ~]# grep -i Firewall anaconda-ks.cfg
```

* Now what if you want to check the word in multiple files at once, or you want to check for all the files in the working directory.
    

```plaintext
[root@localhost ~]# grep -iR Firewall *
#here R means that the command will get into a directory and check there as well.
```

* We have a reader command **less** which will show a file but won't quit like the **cat** command. We can directly give **less &lt;file\_path&gt;**. It looks like a VIM editor, we can also search for words by giving forward Slash + the word **/firewall**.
    
* We have **more** similar to the above **less**, you will have to use the enter key to go forward, it's up to you which you are using. They both serve the same purpose.
    
* In case we want to see the first few lines of a particular file, for this, we can make use of the **head** command, we can give **head &lt;file\_path&gt;**. The opposite of this is the **tail** command to view the end few lines of the file.
    
* If the files are segregated under rows and columns using signs like **: or , or etc** and you want to view only a particular row then we can use the cut command as below.
    

```plaintext
[root@localhost ~]# cut -d: -f1 /etc/passwd

-> here the -d: means separated by : and f1 means the first column
```

* Now the **cut** command is good only if we have a proper separator, in case the file does not have a separator then will use the **awk** command. Where we can make use of the regular expression.
    

```plaintext
[root@localhost ~]# awk -F':' '{print $1}' /etc/passwd
```

* Now let's move on, what if you want to replace a particular word in a file with some other word, one way is by using the vim editor, in the command like you can give **:%s/word\_you\_want\_to\_replace/replacement\_word**, but there is a flaw, if the text is multiple times in a line then it would just replace the first word. If you want to replace it everywhere we can give the command **:%s/word\_you\_want\_to\_replace/replacement\_word/g**
    
* Above work can also be done using the **sed** command.
    

```plaintext
# this command will first print what you are changing 
[root@localhost ~]# sed 's/firewall/FireWall/g' anaconda-ks.cfg 

# now if you want to execute it then you need to give -i
```

## IO redirection

Redirection is a process where we can copy the output of a command, file into a new file. There are two ways of redirecting the output into the file.

* Using **\&gt; or &gt;&gt; filename** after the command
    
* we make use of **\&gt;** in case we want to replace the old file(if there) content with the new one else we make use of **\&gt;&gt;** which will just append at the end of the old file if there else create a new one in both the cases.
    
* If you don't want to see the output also don't want to store it in any other file also then you will send that command output to \*\*&gt; /dev/null \*\* which is like a black hole and everything is saved there, we can't retrieve it back.
    
* There is one other use of the /dev/null file, in case you want to remove the content of any file then simply you need to issue the command **/dev/null &gt; filename**.
    
* We can make use of **'|'** to concatenate 2 different commands, for example, if you issue the command **free -m | grep Mem** then only Mem will be shown out of the whole output from the command free -m.
    
* What if you want to find a file itself then we can make use of the command **find**. let's see an example, you can issue the command \*\* find /etc -name host\*\*.
    

## Users and Groups

Users and groups are used to control access to files and resources. The Users log in to the system by giving their username and password. Every File will be owned by some user and some group with it.

Every user has its own userid which is known as UID. This information is stored in **etc/passwd** and the password is stored in **etc/shadow** in encrypted form.

There are 3 types of users -&gt;

* ROOT User &gt; UID=0 &gt; GID=0 &gt; HOME DIR = /root &gt; SHELL = /bin/bash
    
* REGULAR User &gt; UID=(1000 to 60000) &gt; GID =(1000 to 60000) &gt; HOME DIR = /home/username&gt; SHELL = /bin/bash
    
* SERVICE User &gt; UID = (1 to 999) &gt; GID = (1 to 999) &gt; HOME DIR = /var/ftp etc &gt; SHELL = /sin/nologin
    

There are a few commands that you might want to know.

* to add a user we can give **useradd username**
    
* to view the user information we can give the command **id username**
    
* to create a group we can use the command **groupadd groupname**
    
* to add users to a certain group we can use the command **usermod -aG groupname username** or you can directly edit the group file also by using a comma as a separator you can give as many users you want.
    
* Right now no one would you able to log in using the user you created because first, you have to create a password for the same. We can make use of the command **passwd username** and set a password.. Remember this command can also be used to reset the password and only can be done by the root user.
    
* Now if you want to delete a user you can use the command **userdel username** and delete the group using the **groupdel groupname**.
    

## File Permissions

When you logged in with the root user and you give the command **ls -l**, you might get a result something like the below.

```plaintext
-rw-------. 1 root root 2300 Apr  7 07:42 anaconda-ks.cfg
lrwxrwxrwx. 1 root root   37 Apr  5 06:09 cmds -> /opt/dev/ops/devops/test/commands.txt
-rw-------. 1 root root 1557 Feb 12 17:54 original-ks.cfg
drwxr-xr-x. 2 root root    6 Apr  5 06:05 =p
```

Now let's understand what the output above represents.

* Remember **r means read permission, w means write permission and x means execute permission**
    
* First, let's consider the file **anaconda-ks.cfg** there if you see from the right side the first letter or hyphen represents the type of that file.
    
* Next 3 places which are **'rw-'** will represent User/Owner Permission, which is read and write.
    
* Next 3 places which are **'---'** will represent Group Permission.
    
* Last 3 places which are **'---'** will represent Others Permissions.
    

## Thank-you!

I am glad you made it to the end of this article. I hope you got to learn something, if so please leave a **Like** which will encourage me for my upcoming write-ups.

* [My GitHub Repos](https://github.com/akxat)
    
* Connect with me on [Linkedin](https://www.linkedin.com/in/sharma-akshat/)
    
* Start [your own blogs](https://hashnode.com/@AkshatSharma/joinme)
    

%%[wid-1]