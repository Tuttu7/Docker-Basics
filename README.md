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
#### Downloading Docker Images 
```
[root@ip-172-31-43-110 ~]# docker pull httpd:2.2
2.2: Pulling from library/httpd
f49cf87b52c1: Pull complete 
24b1e09cbcb7: Pull complete 
8a4e0d64e915: Pull complete 
bcbe0eb4ca51: Pull complete 
16e370c15d38: Pull complete 
Digest: sha256:9784d70c8ea466fabd52b0bc8cde84980324f9612380d22fbad2151df9a430eb
Status: Downloaded newer image for httpd:2.2
```
#### Creating httpd Container
```
[root@ip-172-31-43-110 ~]# docker container run --name webserver -d -p 80:80 httpd:2.2
eecca5fc9735e47bbfd2af7e9def05d3cd1cb25e908fe299b76bb01899e0e0a9
```
- -d dettached
- --p port publish
- 8080 host port
- 80 destination Port

#### Docker Exec
```
[root@ip-172-31-43-110 ~]# docker exec webserver ps aux
USER       PID %CPU %MEM    VSZ   RSS TTY      STAT START   TIME COMMAND
root         1  0.5  0.9 212312  9712 ?        Ss   17:11   0:00 httpd -DFOREGROUND
daemon       7  0.0  0.3 212368  3680 ?        S    17:11   0:00 httpd -DFOREGROUND
daemon       8  0.0  0.3 212368  3680 ?        S    17:11   0:00 httpd -DFOREGROUND
daemon       9  0.0  0.3 212368  3680 ?        S    17:11   0:00 httpd -DFOREGROUND
daemon      10  0.0  0.3 212368  3680 ?        S    17:11   0:00 httpd -DFOREGROUND
daemon      11  0.0  0.3 212368  3680 ?        S    17:11   0:00 httpd -DFOREGROUND
root        12  0.0  0.2  17504  2076 ?        Rs   17:12   0:00 ps aux


[root@ip-172-31-43-110 ~]# docker exec -it webserver bash
root@eecca5fc9735:/usr/local/apache2# ps aux
USER       PID %CPU %MEM    VSZ   RSS TTY      STAT START   TIME COMMAND
root         1  0.1  0.9 212312  9712 ?        Ss   17:11   0:00 httpd -DFOREGROUND
daemon       7  0.0  0.3 212368  3680 ?        S    17:11   0:00 httpd -DFOREGROUND
daemon       8  0.0  0.3 212368  3680 ?        S    17:11   0:00 httpd -DFOREGROUND
daemon       9  0.0  0.3 212368  3680 ?        S    17:11   0:00 httpd -DFOREGROUND
daemon      10  0.0  0.3 212368  3680 ?        S    17:11   0:00 httpd -DFOREGROUND
daemon      11  0.0  0.3 212368  3680 ?        S    17:11   0:00 httpd -DFOREGROUND
root        17  1.8  0.3  20248  3240 pts/0    Ss   17:13   0:00 bash
root        22  0.0  0.1  17504  1960 pts/0    R+   17:13   0:00 ps aux
```
#### Stop / Start Container
```
[root@ip-172-31-43-110 ~]# docker image ls -a
REPOSITORY          TAG                 IMAGE ID            CREATED             SIZE
httpd               2.2                 e06c3dbbfe23        23 months ago       171MB

[root@ip-172-31-43-110 ~]# docker stop webserver
webserver

[root@ip-172-31-43-110 ~]# docker start webserver
webserver
```
#### Deleting the Container
```
[root@ip-172-31-43-110 ~]# docker rm webserver
webserver
````
#### Loading Website From the Host
```
cd /tmp ; \
wget https://www.tooplate.com/zip-templates/2116_blugoon.zip ; \
unzip 2116_blugoon.zip ; \
cd ; \
mkdir content ; \
cp -r /tmp/2116_blugoon/*  ./content/


[root@ip-172-31-43-110 ~]# docker container run -d --name webserver -p 80:80 -v /home/ec2-user/content/:/usr/local/apache2/htdocs/  httpd:2.2
0ff3d80aea3ffca831e75b1d3d8a06296561e234686a07b7b83799feba628cdc
```
#### Creating Docker image
````
root@ip-172-31-43-110 ec2-user]# vim Dockerfile
[root@ip-172-31-43-110 ec2-user]# cat Dockerfile
FROM httpd:2.2
COPY ./content/ /usr/local/apache2/htdocs/
CMD ["httpd-foreground"]
[root@ip-172-31-43-110 ec2-user]# ls
content  Dockerfile
[root@ip-172-31-43-110 ec2-user]# docker build -t mysite:1 .
Sending build context to Docker daemon    5.6MB
Step 1/3 : FROM httpd:2.2
 ---> e06c3dbbfe23
Step 2/3 : COPY ./content/ /usr/local/apache2/htdocs/
 ---> 978f12314f49
Step 3/3 : CMD ["httpd-foreground"]
 ---> Running in 4cebf5f42a2e
Removing intermediate container 4cebf5f42a2e
 ---> 3c89f5019e2d
Successfully built 3c89f5019e2d
Successfully tagged mysite:1
````

#### Creating a container with the docker image 
```
[root@ip-172-31-43-110 ec2-user]# docker run -d --name newbuild -p 80:80 mysite:1
c893ff3dca0706dd2b0644975a08b7466607482d0b53e432c2f1ba82aab652bb


[root@ip-172-31-43-110 ec2-user]# docker container ls -a     
CONTAINER ID        IMAGE               COMMAND              CREATED             STATUS              PORTS                NAMES
c893ff3dca07        mysite:1            "httpd-foreground"   47 seconds ago      Up 46 seconds       0.0.0.0:80->80/tcp   newbuild
[root@ip-172-31-43-110 ec2-user]# docker exec newbuild ps aux
USER       PID %CPU %MEM    VSZ   RSS TTY      STAT START   TIME COMMAND
root         1  0.2  0.9 212312  9656 ?        Ss   17:45   0:00 httpd -DFOREGROUND
daemon       7  0.0  0.3 212368  3664 ?        S    17:45   0:00 httpd -DFOREGROUND
daemon       8  0.0  0.3 212368  3664 ?        S    17:45   0:00 httpd -DFOREGROUND
daemon       9  0.0  0.3 212368  3664 ?        S    17:45   0:00 httpd -DFOREGROUND
daemon      10  0.0  0.3 212368  3664 ?        S    17:45   0:00 httpd -DFOREGROUND
daemon      11  0.0  0.3 212368  3664 ?        S    17:45   0:00 httpd -DFOREGROUND
root        12  0.0  0.2  17504  2084 ?        Rs   17:46   0:00 ps aux

[root@ip-172-31-43-110 ec2-user]# docker exec -it newbuild bash
root@c893ff3dca07:/usr/local/apache2# httpd -V
Server version: Apache/2.2.34 (Unix)
Server built:   Jan 18 2018 23:12:10
Server's Module Magic Number: 20051115:43
Server loaded:  APR 1.5.1, APR-Util 1.5.4
Compiled using: APR 1.5.1, APR-Util 1.5.4
Architecture:   64-bit
Server MPM:     Prefork
  threaded:     no
    forked:     yes (variable process count)
Server compiled with....
 -D APACHE_MPM_DIR="server/mpm/prefork"
 -D APR_HAS_SENDFILE
 -D APR_HAS_MMAP
 -D APR_HAVE_IPV6 (IPv4-mapped addresses enabled)
 -D APR_USE_SYSVSEM_SERIALIZE
 -D APR_USE_PTHREAD_SERIALIZE
 -D SINGLE_LISTEN_UNSERIALIZED_ACCEPT
 -D APR_HAS_OTHER_CHILD
 -D AP_HAVE_RELIABLE_PIPED_LOGS
 -D DYNAMIC_MODULE_LIMIT=128
 -D HTTPD_ROOT="/usr/local/apache2"
 -D SUEXEC_BIN="/usr/local/apache2/bin/suexec"
 -D DEFAULT_PIDLOG="logs/httpd.pid"
 -D DEFAULT_SCOREBOARD="logs/apache_runtime_status"
 -D DEFAULT_LOCKFILE="logs/accept.lock"
 -D DEFAULT_ERRORLOG="logs/error_log"
 -D AP_TYPES_CONFIG_FILE="conf/mime.types"
 -D SERVER_CONFIG_FILE="conf/httpd.conf"

 root@c893ff3dca07:/usr/local/apache2# cd /usr/local/apache2/htdocs/
root@c893ff3dca07:/usr/local/apache2/htdocs# ls
ABOUT THIS TEMPLATE.txt  assets  index.html  prepros-6.config  vendor
root@c893ff3dca07:/usr/local/apache2/htdocs# 
```


