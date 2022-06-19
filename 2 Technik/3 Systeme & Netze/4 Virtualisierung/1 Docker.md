# Commands

## Don't use sudo all time:

sudo usermod -aG docker $USER

//replace path with /var/run/docker.socket or the file or folder //that makes problems sudo chown "$USER":"$USER" /home/"$USER"/.docker -R

Beispiel:

sudo chown gabriel:gabriel /var/run/docker.sock -R


### [name]:

docker nickname or id can be used nickname: docker ps -a, last row id: docker ps -a, first row

```ad-success
title: docker ps
show all running containers 

[-a] show also stopped container (all container)
```


```ad-success
title: docker run [name]

create container out of image and runs it 

[-it] -i is interactive and -t is create virtual terminal(tty) to connect 

[--rm] delete container after it got stopped 

[-d] runs container in background [without terminal waiting] 

[-p 6345:22] port forwarding, port 6345 of your computer gets redirected to 22 inside container from other computer it is simply ssh "user@yourip" -p "port" f.e.: ssh root@192.168.1.192 -p 6345 

[-v /host/directory:/container/directory] creates a shared folder with the same files in container and on host

[- -name name] gives the container a custom name
```

```ad-success
title: docker start [name]

start stopped container   
[-i] start interactive with cli (for normal use)
```

```ad-success
title: docker images

show docker images (attention! images, not container)
```

```ad-success
title: docker stop [name]

stop running container
```

```ad-success
title: docker stats

show running container and their stats
```

```ad-success
title: docker rmi [name]

removes docker image 
```

```ad-success
title: docker rm [name]

remove docker container
```

```ad-success
title: docker build . -t [name]

creates Docker images from the directory. Directory must contain Dockerfile [.] Take current directory (searches for Dockerfile).

[-t] Name of image, otherwise the name is "< none >"
```

## Difference between RUN and CMD in Dockerfile

RUN runs commands like installing packages or other things directly when the container gets created. CMD is the same as RUN but it gets executed when the container gets started.


# How it works

## Docker

Docker uses a feature of the Linux kernel, Namespaces . Using namespaces docker can create isolated, so called containers, where the user can execute commands without affecting the running operating system. Before Docker, virtual machines were used. The Problem is that virtual machines virtualize the hardware, so our applications run on a virtual machine and our host os. That uses up a lot of resources. Docker on the other hand enhances the host operating system with a daemon and the applications runs on the host operating system. These containers are isolated, so they cannot break the OS.

## Namespaces

Namespaces is a feature of the Linux kernel. With namespaces you can arrange that some processes see some resources that other processes don't see. There are a few different Namespace kinds:

## Overview

With the linux command lsns we can see all the currently active namespaces. In the type columns we can see the kind of namespace and in the command column we can see the command that is executed. We can see that a lot of namespaces are created by normal applications like chrome and discord. These namespaces are used for a principle called "sandbox". A sandbox isolates the application and improves privacy and security. For example chrome cannot unintentionally cause harm to the OS or to the hardware. It also improves privacy because the application cannot see if other applications are installed or what the user is doing outside of the sandbox.

One of the most used kinds of namespaces is the PID Namespace. The other namespaces work in a similar manner.

A new Namespace is created by calling the unshare syscall ([https://man7.org/linux/man-pages/man2/unshare.2.html](https://man7.org/linux/man-pages/man2/unshare.2.html))

## PID Namespace

The PID namespace is probably the most used Namespaces . This namespace manages the pid numbers given to the processes in each namespace. The pid namespace provides every process with a pid for each namespace the process is in. All the processes are also inside the initial namespace. Other resource on the PID-Namespace: [https://man7.org/linux/man-pages/man7/pid_namespaces.7.html](https://man7.org/linux/man-pages/man7/pid_namespaces.7.html) You can create a new PID namespace by calling unshare with the CLONE_NEWPID flag as an argument:

CLONE\_NEWPID (since Linux 3.8) This flag has the same effect as the [clone(2)](https://man7.org/linux/man-pages/man2/clone.2.html) CLONE\_NEWPID flag. Unshare the PID namespace, so that the calling process has a new PID namespace for its children which is not shared with any previously existing process. The calling process is not moved into the new namespace. The first child created by the calling process will have the process ID 1 and will assume the role of [init(1)](https://man7.org/linux/man-pages/man1/init.1.html) in the new namespace. CLONE\_NEWPID automatically implies CLONE\_THREAD as well. Use of CLONE\_NEWPID requires the CAP\_SYS\_ADMIN capability. For further information, see [pid\_namespaces(7)](https://man7.org/linux/man-pages/man7/pid_namespaces.7.html).

Source: [https://man7.org/linux/man-pages/man2/unshare.2.html](https://man7.org/linux/man-pages/man2/unshare.2.html)
