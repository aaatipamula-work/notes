# UNIX and Linux

*Add info on Linux Distros and systemctl, ufw apt-get/apt for ubuntu, selinux firewalld and dnf for fedora.*

## Overview

[UNIX](https://en.wikipedia.org/wiki/Unix) is the godfather of about 90% of all modern OSes. Developed a group of computer science researchers at AT&T's Bell Labs, they developed the basic filesystem structure and many of the basic programs we use in most OSes today. Although first written in assembly for specific computers, it was eventually written in [C](https://en.wikipedia.org/wiki/C_(programming_language)) and made portable, which was a major step towards it gaining popularity. 

### Derivatives of UNIX

Eventually other projects with modifications to the UNIX OS started to appear. 

[BSD](https://en.wikipedia.org/wiki/Berkeley_Software_Distribution) or Berkley Software Distribution was originally just a superset of Unix and implemented the first TCP/IP protocol. It eventually became the father of two other OSes that are fairly popular in the modern age, [MacOS](https://en.wikipedia.org/wiki/MacOS) and [FreeBSD](https://en.wikipedia.org/wiki/FreeBSD). There were some other popular OSes that came from Unix/BSD which eventually lost popularity such as [SunOS](https://en.wikipedia.org/wiki/SunOS) and [Solaris](https://en.wikipedia.org/wiki/Oracle_Solaris). 

### The Rise of Linux

The problem with UNIX and most other UNIX-like OSes is they were all paid for and proprietary software. While some projects such as *BSD* were already pushing to make their software completely open source, Linux came in as one of the first completely open source and free to use software that ported over many of the Unix utilities and structure.

This was accomplished mostly by the [GNU](https://en.wikipedia.org/wiki/GNU) project as they collected and wrote the core programs that most operating systems at the time used. They then released that collection of programs under a [GNU General Public License](https://en.wikipedia.org/wiki/GNU_General_Public_License) or GPL which allowed for sharing, modification and commercial use of the software. At the time the project was only missing an operating system kernel to tie everything together. This is where [Linus Torvalds](https://en.wikipedia.org/wiki/Linus_Torvalds) comes in. Linus was a Swedish software developer who first wrote what came to be known as the Linux kernel for a personal computer. He later published it for people to share, but not under the GNU license. Eventually after attending a speech by [Richard Stallman](https://en.wikipedia.org/wiki/Richard_Stallman), the founder of the GNU organization, he changed his kernel's license to the GNU GPL. From there it was only a matter of time that the kernel became widely adopted. 

The heavy involvement of GNU in the creation of what became widely known as Linux is why you'll sometimes see people correct you and say it should be called "GNU-Linux".

> Fun note, the name Linux only came about as Linus' friend who hosted the FTP server that held the kernel named his directory "linux".

### Minix

A different OS named [Minix](https://en.wikipedia.org/wiki/Minix) actually came out before Linux that was free and open source. It was created by professor [Andrew S. Tanenbaum](https://en.wikipedia.org/wiki/Andrew_S._Tanenbaum) who wrote the program as a way for students to learn Unix. It came packaged with a textbook but was also distributed for free to universities. While this OS predated the Linux kernel it never gained popularity as it was not designed for commercial use, while the GNU project had commercial use in mind.

It's a very cool project, only 12,000 lines of C code for a fully functional OS and uses a different kernel architecture as compared to Linux ([microkernel](https://en.wikipedia.org/wiki/Microkernel) v.s. [monolithic kernel](https://en.wikipedia.org/wiki/Monolithic_kernel)). It still has some use today and Intel has even been found to use it in their CPUs.

### POSIX

With the prevalence of UNIX-like operating systems the [IEEE](https://en.wikipedia.org/wiki/Institute_of_Electrical_and_Electronics_Engineers) decided to standardize how OSes and applications interact to make porting applications and OSes much easier. POSIX (Portable Operating System Interface) is also a trademark owned by the IEEE so operating systems can be POSIX certified. While many OSes follow the POSIX standard, the only commercially used OS that is POSIX certified is MacOS (ironically).

## Commands 

The following are commands that should appear in any UNIX-like OS. Most of them are basic commands but there are some useful ones I've also listed out. 

The simpler and common commands are grouped by similarity. The more complex commands have their own sections.

### I/O

| Command | Description | Notes |
| --- | --- | --- | 
| `cat` | List the contents of a text encoded file | |
| `head` | List the first 10 lines of a text encoded file | You can specify how many lines to print 10 is the default |
| `tail` | List the last 10 lines of a text encoded file | You can specify how many lines to print 10 is the default |
| `less` | List the contents of a file in a navigable format | Use *j* and *k* to move up and down |
| `|` | Pipe the output of the command on the left to the command on the right | e.g. `history | grep python` | 
| `>` | Write the output of a command to a file | e.g. `ps -ef > processes.txt` | 
| `>>` | Append the output of a command to a file | e.g. `ps -ef >> processes.txt` | 
| `grep` | Search for a word or pattern in files or text | Uses basic regex and some extended regex |

### Processes

| Command | Description | Notes |
| --- | --- | --- | 
| `ps` | List running processes | I use it commonly with `-ef` to list more information and processes from all users |
| `top` | List all running processes and system info in an interactive way | |
| `htop` | List all running processes and system info in a more interactive way | More color output and has some other system info |
| `kill` | Kill a process from a process id | |
| `nohup` | No hangup; Unless the process is specifically sent a kill signal do not end the process | Useful if you want to start a command in a terminal session and exit the session, e.g. `nohup sleep 100` |
| `&` | Run a command in the background | Append this to the end of your command, e.g. `sleep 100 &` |
| `CTRL-Z` | Stop a command | | 
| `jobs` | List active or stopped commands | |
| `bg` | Continue running a job in the background | Append `%` to the job number, e.g `fg %1` to run job 1 in the foreground |
| `fg` | Continue running a job in the foreground | Append `%` to the job number, e.g `bg %1` to run job 1 in the background |

### Filesystem

| Command | Description | Notes |
| --- | --- | --- | 
| `pwd` | Print the current directory you are in | |
| `cd` | Change directories | `.` and `..` are special directories that point to the current directory and the directory one jump up respectively. You can move one directory up by using `cd ..` |
| `ls` | List the files and directories of a directory; defaults to current directory `.` | Adding the `-lh` flags gives more useful information on files in a human readable format. The `-a` flag lists hidden directories and files. |
| `cp a b` | Copy file `a` into file `b` | Add the `-r` flag to copy directories and their contents |
| `rmdir` | Remove an *empty* directory | |
| `rm` | Remove a file | Add the `-rf` flags to remove non empty directories **WARNING**: Do NOT run `rm -rf /` it will crash your system almost irreparably. |
| `mv a b` | Move a file `a` to file `b` | This also works on directories |
| `touch a` | Create a file `a` | |
| `mkdir a` | Create a directory `a` | |
| `chown user ./file.txt` | Change the owner of `file.txt` to `user` | Add the `-R` flag to have it apply recursively to a directory |
| `chgrp group ./file.txt` | Change the group owner of `file.txt` to `user` | Add the `-R` flag to have it apply recursively to a directory |
| `chmod 777 ./file.txt` | Change read, write and execute permissions of `file.txt` | Check [Chmod Octal Chart](#chmod-octal-chart) for how to specify file permissions |

### User

| Command | Description | Notes |
| --- | --- | --- | 
| `useradd` | Add a user | Use the `-D` flag for default options. |
| `passwd` | Give a user a password | |
| `su` | Switch user | Use `sudo su` to switch to the super user for multiple commands |

### Extras

| Command | Description | Notes |
| --- | --- | --- | 
| `sudo` | Run a command as the super user or 'admin' | Add the `-e` flag to edit a file as sudo. You must have sudo (admin) permissions to use this command. |
| `man` | Get a detailed help page on a command and its options. | |
| `whatis` | Get a short description of a command | |
| `clear` | Clear the screen of previous commands and output | |

### SSH

[SSH](https://en.wikipedia.org/wiki/Secure_Shell) is a program that allows us to easily access Linux machines form the command line remotely. Almost anything that can be done on the machine locally can be done from SSH.

#### SSH-Client

An SSH connection can be invoked something similar to the following:

```bash
ssh user@host
```

`user` being the username of the user you would like to connect to on the remote server and `host` being the IP address or domain name of the remote server.

If the SSH server is running on a different port *e.g. port 8100* the `-p` flag can be appended as following:

```bash
ssh user@host -p 8100
```

If you are using an key that is not named `id_rsa.pub` you can specify the public key with the `-i` flag:

```bash
ssh user@host -i /path/to/pubkey
```

##### SSH Config

SSH has a configuration file that can be found at `~/.ssh/config`. The formatting of a config file would be similar to the following:

```ssh
Host hostname1
  HostName www.example.com
  User user
  Port 8100
  IdentityFile /path/to/pubkey
```

With that file set the command `ssh hostname1` will iniatate a connection with all the parameter set for `hostname1`. 

This file can be expanded to as many hosts as you would like and can even be configured with basic regex to match certain parameters.

Read more about ssh config [here](https://www.ssh.com/academy/ssh/config)

##### SSH Keys

SSH Has a more secure method of authentication than user and password. This is called SSH keys. One can be generated by using the following command and following the instructions:

```bash
ssh-keygen
```

I usually add the flags `-t rsa -b 4090` to specify the rsa encryption algorithm and generate a longer key.

#### SSH-Server

The SSH server configuration can be found at `/etc/ssh/sshd_config`. 

I usually set the following parameters:

```
PermitRootLogin no
PasswordAuthentication no
Port 10023
```

Read more about the `ssh_config` file [here](https://www.ssh.com/academy/ssh/sshd_config)

### Crontab

Crontab is a program that is useful to run commands on a schedule. It uses a simple config file that can be accessed by running:

```
crontab -e
```

When the config file is open, you can add a scheduled job by using the following syntax:

```
MIN HR DOM MONTH DOW /path/to/command/or/script
```

| Field | Description | Valid Values |
| --- | --- | --- |
| MIN | Minute of the Day | 0-59 |
| HR | Hour of the Day | 0-23 |
| DOM | Day of the Month | 1-31 |
| Month | Month of the Year | 1-12 |
| DOW | Day of the Week | 0-6 |

e.g. Run a backup script at every 1st minute. (Runs the first minute of every hour of the day 24/7, 356 days a year.):

```
1 * * * * /home/user/backup.sh
```

It can get a little complex but I suggest looking at [Crontab Guru](https://crontab.guru/) to get some practice and check your scheduling syntax.

**Note**: It is suggested to use the full path of scripts and files you would like to run.

**Note**: Don't run sudo commands!

### Chmod Octal Chart

| Octal | Binary | File Mode | 
| --- | --- | --- |
| 0 | 000 | \-\-\- |
| 1 | 001 | --x |
| 2 | 010 | -w- |
| 3 | 011 | -wx |
| 4 | 100 | r-- |
| 5 | 101 | r-x |
| 6 | 110 | rw- |
| 7 | 111 | rwx |

If you run `ls -l` you will see each file prepended with something similar to the following:

```
-rw-r--r-- 
```

These are the read, write and execute permissions for the file to the owner of the file, group owner of the file, and everyone else. This can be modified using the `chmod` command. 

After flags are given to the command the second to last argument of the chmod command is an *octal number representation of the permissions* you would like to give the file. *Each of the 3 numbers corresponds to the file owner permissions, group owner permissions, and any user permissions respectively.* This is also reflected in the ls command with each grouping of three characters minus the very first character which indicates if the file is a directory or not. Refer to the **octal chart** above to find the correct octal number representation of file permissions for the user, group and everyone else.

## Shells

Common Shells:
- [Bash](#bash)
- Zsh
- Fish
- PowerShell

Less Common:
- Sh
- Ksh
- Csh

### Common Functionality

The following is functionality that most modern shells have.

- History
- Settings
- Autocomplete/Suggestion
- I/O redirection
- [Scripting](./languages/shellscript.md)

### Bash

Bash, or the Bourne-Again Shell is the most prevalent shell in today's world. It is partly due to the fact that UNIX-like and Linux operating systems are often shipped with it. 

#### Configuration

Bash has a fair bit of configuration you can do. This is done by either creating or modifying one of the following files in your `$HOME` directory:

- `.bash_profile`
- `.bash_login`
- `.profile`
- `.bashrc`*

\***Note**: If bash is invoked with the *login* option it will look for and execute the first three files previously listed *in that order*. If the *login* option is not set, bash will look for the `.bashrc` file. So by convention most configuration is done in the `.bashrc` file and that file is then called from `.bash_profile`.

##### Aliases

Aliases can be defined in one of the configuration files and are defined as following:

```bash
alias ls="ls -lh"
```

This is useful for setting common options on frequently used commands or making long commands shorter.

**Note**: For both [Aliases](#aliases) and [Environment Variables](#environment-variables) adding spaces between the `=` character can lead to parsing errors.

##### Environment Variables

These can be set to use globally in bash:

```bash
export filepath="/path/to/file"
```

I use this for setting common filepaths but it can also be used to clean up your home directory.

**Note**: For both [Aliases](#aliases) and [Environment Variables](#environment-variables) adding spaces between the `=` character can lead to parsing errors.

#### History Expansion

A few bash history commands I find useful.

| Command | Description | Notes |
| --- | --- | --- | 
| `up` | The up arrow cycles through your most recently run command from newest to oldest. | | 
| `history` | Lists all the commands saved in history prepended with a number to reference the command. | |
| `!!` | Run the most recent command. | Useful when you forget to prepend a sudo e.g. `sudo !!` |
| `!*` | Get all the options from the most recent command | If the previous command was `cat ./file.txt` and you want to open it try `vim !*` |
| `!foo` | Get the most recent command *starting* with `foo` and run it | |
| `!?foo` | Get the most recent command that *containing* `foo` and run it | |
| `!n` | Run the nth command in your history | Negate `n` to reverse search and run the nth most recent command |
| `!!:n` | Get the nth option from the most recent command | If the previous command was `ls -la /home` and you want to change directories try `cd !!:2`; Replace `n` with `$` for the last argument; Select ranges with a colon between numbers, e.g. `!!:2-$` | 

Refer to [this](https://www.thegeekstuff.com/2011/08/bash-history-expansion/) guide for more detailed info.

## Linux Distributions
