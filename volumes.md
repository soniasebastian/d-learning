# Docker Volumes

## Problem Statement

It is a very common requirement to persist the data in a Docker container beyond the lifetime of the container. However, the file system
of a Docker container is deleted/removed when the container dies. 

## Solution

There are 2 different ways how docker solves this problem.

1. Volumes
2. Bind Directory on a host as a Mount

### Volumes 

Volumes aims to solve the same problem by providing a way to store data on the host file system, separate from the container's file system, 
so that the data can persist even if the container is deleted and recreated.

![image](https://user-images.githubusercontent.com/43399466/218018334-286d8949-d155-4d55-80bc-24827b02f9b1.png)


Volumes can be created and managed using the docker volume command. You can create a new volume using the following command:

```
docker volume create <volume_name>
```

Once a volume is created, you can mount it to a container using the -v or --mount option when running a docker run command. 

For example:

```
docker run -it -v <volume_name>:/data <image_name> /bin/bash
```

This command will mount the volume <volume_name> to the /data directory in the container. Any data written to the /data directory
inside the container will be persisted in the volume on the host file system.

### Bind Directory on a host as a Mount

Bind mounts also aims to solve the same problem but in a complete different way.

Using this way, user can mount a directory from the host file system into a container. Bind mounts have the same behavior as volumes, but
are specified using a host path instead of a volume name. 

For example, 

```
docker run -it -v <host_path>:<container_path> <image_name> /bin/bash
```

## Key Differences between Volumes and Bind Directory on a host as a Mount

Volumes are managed, created, mounted and deleted using the Docker API. However, Volumes are more flexible than bind mounts, as 
they can be managed and backed up separately from the host file system, and can be moved between containers and hosts.

In a nutshell, Bind Directory on a host as a Mount are appropriate for simple use cases where you need to mount a directory from the host file system into
a container, while volumes are better suited for more complex use cases where you need more control over the data being persisted
in the container.


CLASS EXPLANATION

PROBLEM 1 : container...ngnix.application inside container..puts user information/ip address accessed.....ngnix stores in logfile.....security auditing ....
last 10 days information.....
container goes down.....log file gets deleted ...conatiners are ephemeral in nature/shortlived/light-weighted
cpu/memory/storage/file system used from kernal/host system
user details/log file gets deleted org doesnt have any information to track user detals/etc.


PROBLEM2: There is frontend and backend (flipkart)...filein Json/dynamic html served by frontend..
backend goes down....you didnt have Persistent file storage...entire informn...frontend can only read today records....

PROBLEM3: One application reads files provided from cron job (periodical job) on host...files created..json/yaml/xml container reads file and display to user..
conainer can access CPU/RMA/RESOURCES FROM HOST OS no std way specific directory/folders

TWO SOLUTIONS
1.BIND MOUNTS
2. VOLUMES

1. Bind mounts binds folder/dir on container with a folder on the host .../app in both....
   any file on host can be read from host....

   binding specific directory/folder on the host to ones in the conatiners..

2. Volumes...OFFER BETTER Lifecycle...USING VOLUMES USING Docker CLI....COMMANDS create volumes///logical partition
   create vol/destroy vol/taake one vol from C1 to C2

   not providing directory details
   but asks docker to crate a specific volume
   df....disk.....logical vol


   managing entire thing using a Lifecycle

   advantage of using volumes....bind one dir from host to container....external sources.....
   Host doesnt have enough disk...Back-up safe....mount using external storage devices
   share infor from one container to next
   high performance...
   high I/O 
   



