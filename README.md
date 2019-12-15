#### Docker Installation :
```
yum install docker -y
usermod -a -G docker ec2-user
service docker restart
chkconfig docker on
```
#### Docker Version
```
[root@ip-172-31-47-171 ~]# docker version
Client:
 Version:           18.09.9-ce
 API version:       1.39
 Go version:        go1.10.3
 Git commit:        039a7df
 Built:             Fri Nov  1 19:26:49 2019
 OS/Arch:           linux/amd64
 Experimental:      false

Server:
 Engine:
  Version:          18.09.9-ce
  API version:      1.39 (minimum version 1.12)
  Go version:       go1.10.3
  Git commit:       039a7df
  Built:            Fri Nov  1 19:28:24 2019
  OS/Arch:          linux/amd64
  Experimental:     false          
  ```
  #### Downloading Docker Images
  - Images are pull from https://hub.docker.com
  ```
[root@ip-172-31-47-171 ~]# docker pull ubuntu:16.04                                                                                                  
16.04: Pulling from library/ubuntu
976a760c94fc: Pull complete 
c58992f3c37b: Pull complete 
0ca0e5e7f12e: Pull complete 
f2a274cc00ca: Pull complete 
Digest: sha256:e10375c69cf9e22989c82b0a87c932a21e33619ee322d6c7ce6a61456f54c30c
Status: Downloaded newer image for ubuntu:16.04
```

#### Listing Docker Images 

```
[root@ip-172-31-47-171 ~]# docker images
REPOSITORY          TAG                 IMAGE ID            CREATED             SIZE
ubuntu              16.04               56bab49eef2e        2 weeks ago         123MB
```
#### Creating container
```
[root@ip-172-31-47-171 ~]# docker container run ubuntu:16.04 uptime
 15:07:08 up 7 min,  0 users,  load average: 0.02, 0.05, 0.01

 
 [root@ip-172-31-47-171 ~]# docker container run ubuntu:16.04 w
 15:07:35 up 7 min,  0 users,  load average: 0.01, 0.04, 0.01
USER     TTY      FROM             LOGIN@   IDLE   JCPU   PCPU WHAT
```
#### Listing Container
```
[root@ip-172-31-47-171 ~]# docker container ls
CONTAINER ID        IMAGE               COMMAND             CREATED             STATUS              PORTS               NAMES
[root@ip-172-31-47-171 ~]# docker container ls -a
CONTAINER ID        IMAGE               COMMAND             CREATED              STATUS                          PORTS               NAMES
f73f1d3720c7        ubuntu:16.04        "w"                 57 seconds ago       Exited (0) 55 seconds ago                           naughty_kowalevski
da11bbf4d755        ubuntu:16.04        "uptime"            About a minute ago   Exited (0) About a minute ago                       loving_elgamal
```

#### Removing Existed containers

```
[root@ip-172-31-47-171 ~]# docker container rm f73f1d3720c7
f73f1d3720c7

[root@ip-172-31-47-171 ~]# docker container ls -a
CONTAINER ID        IMAGE               COMMAND             CREATED             STATUS                     PORTS               NAMES
da11bbf4d755        ubuntu:16.04        "uptime"            2 minutes ago       Exited (0) 2 minutes ago                       loving_elgamal
[root@ip-172-31-47-171 ~]# 


[root@ip-172-31-47-171 ~]# docker rm loving_elgamal
loving_elgamal
[root@ip-172-31-47-171 ~]# docker container ls -a
CONTAINER ID        IMAGE               COMMAND             CREATED             STATUS              PORTS               NAMES
```
#### Creating Bash process
```
[root@ip-172-31-47-171 ~]# docker run --name example -it ubuntu:16.04 bash
root@fa646220e6e7:/# ls /
bin  boot  dev  etc  home  lib  lib64  media  mnt  opt  proc  root  run  sbin  srv  sys  tmp  usr  var
root@fa646220e6e7:/# ps aux
USER       PID %CPU %MEM    VSZ   RSS TTY      STAT START   TIME COMMAND
root         1  1.0  0.3  18236  3260 pts/0    Ss   15:11   0:00 bash
root        11  0.0  0.2  34424  2860 pts/0    R+   15:11   0:00 ps aux


[root@ip-172-31-47-171 ~]# docker ps -a
CONTAINER ID        IMAGE               COMMAND             CREATED              STATUS                     PORTS               NAMES
fa646220e6e7        ubuntu:16.04        "bash"              About a minute ago   Exited (0) 8 seconds ago                       example


[root@ip-172-31-47-171 ~]# docker ps -a
CONTAINER ID        IMAGE               COMMAND             CREATED             STATUS              PORTS               NAMES
fa646220e6e7        ubuntu:16.04        "bash"              2 minutes ago       Up 12 seconds                           example
```

#### Starting Stopped Container
```
[root@ip-172-31-47-171 ~]# docker start example
example
[root@ip-172-31-47-171 ~]# docker ps -a
CONTAINER ID        IMAGE               COMMAND             CREATED             STATUS              PORTS               NAMES
fa646220e6e7        ubuntu:16.04        "bash"              2 minutes ago       Up 12 seconds                           example

[root@ip-172-31-47-171 ~]# docker attach example
root@fa646220e6e7:/# ^C
root@fa646220e6e7:/# w
 15:24:21 up 24 min,  0 users,  load average: 0.04, 0.04, 0.01
USER     TTY      FROM             LOGIN@   IDLE   JCPU   PCPU WHAT
root@fa646220e6e7:/# ps aux
USER       PID %CPU %MEM    VSZ   RSS TTY      STAT START   TIME COMMAND
root         1  0.0  0.3  18232  3296 pts/0    Ss   15:13   0:00 bash
root        11  0.0  0.2  34424  2820 pts/0    R+   15:24   0:00 ps aux
```

