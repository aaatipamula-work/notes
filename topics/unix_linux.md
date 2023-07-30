# UNIX and Linux

*Add sections on bash and commands*

## Overview

[UNIX](https://en.wikipedia.org/wiki/Unix) is the godfather of about 90% of all OSes, developed a group of people at AT&T's Bell Labs, that group of computer scientists developed the filesystem structure and many of the basic programs we use in most OSes today. Although first written in assembly for specific computers, it was eventually written in C and made portable, which was a major step towards it gaining popularity. 

### Derivatives of UNIX

Eventually other projects with modifications to the UNIX OS started to appear. 

[BSD](https://en.wikipedia.org/wiki/Berkeley_Software_Distribution) or Berkley software  was originally just a superset of Unix and implemented the first TCP/IP protocol. It eventually became the father of two other OSes that are fairly popular in the modern age, [MacOS](https://en.wikipedia.org/wiki/MacOS) and [FreeBSD](https://en.wikipedia.org/wiki/FreeBSD). There were some other popular OSes that came from Unix/BSD which eventually died out such as [SunOS](https://en.wikipedia.org/wiki/SunOS) and [Solaris](https://en.wikipedia.org/wiki/Oracle_Solaris). 

### The Rise of Linux

The problem with UNIX and UNIX-like OSes is they were all paid for and proprietary software. While some projects such as *BSD* were already pushing to make their software completely open source, Linux came in as one of the first completely open source and free to use software that ported over many of the Unix utilities and structure.

This was accomplished mostly by the [GNU](https://en.wikipedia.org/wiki/GNU) project as they collected and wrote the core programs that most operating systems used. They then release that collection of programs under a [GNU GPL](https://en.wikipedia.org/wiki/GNU_General_Public_License) or GNU General Public License which allowed for sharing, modification and commercial use of the software. At the time the project was only missing an operating system kernel to tie everything together. This is where [Linus Torvalds](https://en.wikipedia.org/wiki/Linus_Torvalds) comes in. Linus was a Swedish software developer who first wrote the kernel for a personal computer. He later published it for people to share, but not under the GNU license. Eventually after attending a speech by [Richard Stallman]() the founder of the GNU organization he changed his kernel's license to the GNU GPL. From there it was only a matter of time as the kernel became widely adopted. 

The heavy involvement of GNU in the creation of what became widely known as Linux is why you'll sometimes see people correct you and say it should be called "GNU-Linux"

> Fun note, the name Linux only came about as his friend who hosted the FTP server that held the kernel named Linus' directory "linux".

### Minix

A different OS named [Minix](https://en.wikipedia.org/wiki/Minix) actually came out before Linux that was free and open source. It was created by professor [Andrew S. Tanenbaum](https://en.wikipedia.org/wiki/Andrew_S._Tanenbaum) who wrote the program as a way for students to learn Unix. It came packaged with a textbook but was also distributed for free to universities. While this OS predated the GNU project it never gained popularity as it was not designed for commercial use as the GNU project intended.

It's a very cool project, only 12,000 lines of C code for a fully functional OS and uses a different kernel architecture as compared to Linux ([microkernel](https://en.wikipedia.org/wiki/Microkernel) v.s. [monolithic kernel](https://en.wikipedia.org/wiki/Monolithic_kernel)). It still has some use today and Intel has even been found to use it in their CPUs.

### POSIX

With the prevalence of UNIX-like operating systems the [IEEE](https://en.wikipedia.org/wiki/Institute_of_Electrical_and_Electronics_Engineers) decided to standardize how OSes and applications interact to make porting applications and OSes much easier. POSIX (Portable Operating System Interface) is also a trademark owned by the IEEE so operating systems can be POSIX certified. While many OSes follow the POSIX standard the only commercially used OS that is POSIX certified is MacOS (ironically).

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
- Scripting

### Bash

#### Scripting

*Coming Soon*

#### Configuration

Bash has a fair bit of configuration you can do. This is done by either creating or modifying one of the following files in your `$HOME` directory:

- `.bash_profile`
- `.bash_login`
- `.profile`
- `.bashrc`

**Note**: If bash is invoked with the *login* option it will look for and execute the first three files previously listed. If the *login* option is not set, bash will look for the `.bashrc` file. So by convention most configuration is done in the `.bashrc` file and that file is then called from `.bash_profile`.

*More Coming Soon*