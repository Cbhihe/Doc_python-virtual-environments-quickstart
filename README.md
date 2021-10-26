## Tutorial: Python Virtual Environments
#### - QuickStarti in the form of a gentle introduction for Linux users and a few others

Last update: Oct. 2021<BR>
Copyright (c) 2019, 2020, 2021 Cedric Bhihe<BR>
Permission is granted to copy, distribute and/or modify this document,
under the terms of the [GNU Free Documentation License Version 1.3](https://www.gnu.org/licenses/fdl-1.3.txt) or
or any later version published by the Free Software Foundation. You can
consult the full licensing terms either on the Free Software Foundation
web site, or in the adjoined LICENSE.md file.



The decision to write this tutorial can be traced back to two posts: the first is
a 2019 [blog post](https://bartek-blog.github.io/python/2018/08/18/Pyenv-and-VirtualEnvs.html) by Bartek
Skorulski, the second is a 2017 [post](https://stackoverflow.com/a/41573588/4906636) by @Flimm on the Stackoverflow site.
The underlying motivation was my being fed up with the fact that no easy-to-read
even half comprehensive quickstart existed, which tends to make the life of
beginners always more difficult than it should be.

In this tutorial I focus on the environment commonly seen by Archlinux users,
and by extension by all Linux users whose distribution runs on the system and
service initialization manager (1): systemd. This tutorial goes beyond what is
usually seen on the Internet, mostly disjoint commentaries, which many times
can truly be understood only by people who already are experienced Python
virtual environment practitioners. It addresses the down-to-earth needs of both
first-time users and users who want to get a sense of the current Python virtual
environment landscape for Linux (as of mid 2020).

I tried to write in plain English avoiding undue technicalities, so readers can
get to work rapidly. I also tried to provide clean shell code snippet or Bash cli
instructions, meant to be copied and pasted by you in your terminal. Note that
your mileage may vary depending on your Linux distribution and perhaps also on
your shell and shell version. All shell cmds were tested in Bash on CentOS 7.x,
Ubuntu 18.04 and up-to-date Archlinux.

So what is a Python virtual environment and what could motivate the creation of
virtual environments for Python? I answer those two questions superficially in
this introductory section and chose to dedicate the rest of the document to how
one may go about creating and managing virtual environments.

If you use Python for anything, either professionally or at home, chances are
you already ran into snags related to the need for different versions of the same
Python module(s). If you have not yet contended with such predicament, the
premise to this tutorial is that sooner or later you will. This tutorial is a
step-by-step guide on how to overcome such a difficulty by using Python virtual
environments. There are several ways to do so and you may choose the one that
appears more practical to you.

At its root the issue for any programmer is that different versions of any
Python module normally cannot coexist in a single runtime environment (RTE)
and name space. If you did not already tweak your python setup, you may at most
have the latest versions of Python2 (v. 2.7.16) and some version of Python3
installed side by side in your environment. But what if you also needed versions
(say 3.5.4 ***and*** 3.8.0 ***and*** 2.7.1 ***and*** 2.5.0) for a specific project
involving older libraries ?  Forcefully installing any older Python version on
your platform would normally require you to rebuild older packages on a massive
scale, as well as to roll back your system’s module versions and many of its
applications. It can be done but it would be extraordinarily complicated, not
least because it would be very time consuming and prone to breakage. As for
installing several such versions side by side, simply forget it. So how does one
remain practical ? One way is to embrace the concept of Python virtual environments.

A virtual environment is an isolated Python environment, at a specific location (in
a specific directory).  At that location (in that specific directory) you can
install and execute a Python version of your choice, independently of other Python
virtual environments already residing on your platform. The relevant [Arch wiki](https://wiki.archlinux.org/title/Python/Virtual\_environment) explains:<BR>
>  *A virtual environment is a directory in which some binaries and shell scripts
>  are installed. The binaries include python for executing scripts and pip for
>  installing other modules within the environment. There are also shell scripts
>  (at least one for bash, ...) to activate the environment. Essentially, a virtual
>  environment mimics a full system install of Python and all of the desired modules
>  without interfering with any system on which the application might run.*

In this tutorial we will use the abbreviation _VE(s)_, to refer to the term
“virtual environment(s)”.

__________________________________
(1) A simplified overview of the entire Linux boot and startup process is:
1. At host’s power-up, the BIOS does minimal hardware tests and initialization.
      It then hands control over to the boot loader.
2. The boot loader calls the kernel.s
3. The kernel loads an initial RAM disk that loads the system drives and
      then looks for the root file system.
4. After kernel set up, systemd initialization starts.
5. Finally systemd takes over and continues to mount the host’s file systems
      and start services.
