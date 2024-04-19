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


        docker -v
   (attach volume,,pass all in same command)
   
      docker --mount
   (verbose.....more options passed)...specific and simple

   both are same....


PRACTICAL DEMO

docker volume ls
DRIVER    VOLUME NAME

docker volume create sonia
sonia/create a volume

$ docker volume ls
DRIVER    VOLUME NAME
local     sonia

 $ docker volume inspect sonia
[
    {
        "CreatedAt": "2024-04-19T14:46:53Z",
        "Driver": "local",
        "Labels": null,
        "Mountpoint": "/var/lib/docker/volumes/sonia/_data",
        "Name": "sonia",
        "Options": null,
        "Scope": "local"

docker volume rm sonia
sonia// delete multiple volumes

$ docker build -t volumedemo .
$ docker volume create sonia  
docker run -d --mount source=sonia,target=/app nginx:latest
120a02ba807fff2e72a676a6623cb63a80bacd8d2ab0953cd59faad1a0f68394
docker ps
CONTAINER ID   IMAGE          COMMAND                  CREATED              STATUS              PORTS     NAMES
120a02ba807f   nginx:latest   "/docker-entrypoint.…"   About a minute ago   Up About a minute   80/tcp    tender_lamarr

$ docker inspect 120a02ba807f 
[
    {
        "Id": "120a02ba807fff2e72a676a6623cb63a80bacd8d2ab0953cd59faad1a0f68394",
        "Created": "2024-04-19T15:07:48.01526495Z",
        "Path": "/docker-entrypoint.sh",
        "Args": [
            "nginx",
            "-g",
            "daemon off;"
        ],
        "State": {
            "Status": "running",
            "Running": true,
            "Paused": false,
            "Restarting": false,
            "OOMKilled": false,
            "Dead": false,
            "Pid": 17560,
            "ExitCode": 0,
            "Error": "",
            "StartedAt": "2024-04-19T15:07:48.71408422Z",
            "FinishedAt": "0001-01-01T00:00:00Z"
        },
        "Image": "sha256:2ac752d7aeb1d9281f708e7c51501c41baf90de15ffc9bca7c5d38b8da41b580",
        "ResolvConfPath": "/var/lib/docker/containers/120a02ba807fff2e72a676a6623cb63a80bacd8d2ab0953cd59faad1a0f68394/resolv.conf",
        "HostnamePath": "/var/lib/docker/containers/120a02ba807fff2e72a676a6623cb63a80bacd8d2ab0953cd59faad1a0f68394/hostname",
        "HostsPath": "/var/lib/docker/containers/120a02ba807fff2e72a676a6623cb63a80bacd8d2ab0953cd59faad1a0f68394/hosts",
        "LogPath": "/var/lib/docker/containers/120a02ba807fff2e72a676a6623cb63a80bacd8d2ab0953cd59faad1a0f68394/120a02ba807fff2e72a676a6623cb63a80bacd8d2ab0953cd59faad1a0f68394-json.log",
        "Name": "/tender_lamarr",
        "RestartCount": 0,
        "Driver": "overlay2",
        "Platform": "linux",
        "MountLabel": "",
        "ProcessLabel": "",
        "AppArmorProfile": "docker-default",
        "ExecIDs": null,
        "HostConfig": {
            "Binds": null,
            "ContainerIDFile": "",
            "LogConfig": {
                "Type": "json-file",
                "Config": {}
            },
            "NetworkMode": "default",
            "PortBindings": {},
            "RestartPolicy": {
                "Name": "no",
                "MaximumRetryCount": 0
            },
            "AutoRemove": false,
            "VolumeDriver": "",
            "VolumesFrom": null,
            "ConsoleSize": [
                34,
                183
            ],
            "CapAdd": null,
            "CapDrop": null,
            "CgroupnsMode": "private",
            "Dns": [],
            "DnsOptions": [],
            "DnsSearch": [],
            "ExtraHosts": null,
            "GroupAdd": null,
            "IpcMode": "private",
            "Cgroup": "",
            "Links": null,
            "OomScoreAdj": 0,
            "PidMode": "",
            "Privileged": false,
            "PublishAllPorts": false,
            "ReadonlyRootfs": false,
            "SecurityOpt": null,
            "UTSMode": "",
            "UsernsMode": "",
            "ShmSize": 67108864,
            "Runtime": "runc",
            "Isolation": "",
            "CpuShares": 0,
            "Memory": 0,
            "NanoCpus": 0,
            "CgroupParent": "",
            "BlkioWeight": 0,
            "BlkioWeightDevice": [],
            "BlkioDeviceReadBps": [],
            "BlkioDeviceWriteBps": [],
            "BlkioDeviceReadIOps": [],
            "BlkioDeviceWriteIOps": [],
            "CpuPeriod": 0,
            "CpuQuota": 0,
            "CpuRealtimePeriod": 0,
            "CpuRealtimeRuntime": 0,
            "CpusetCpus": "",
            "CpusetMems": "",
            "Devices": [],
            "DeviceCgroupRules": null,
            "DeviceRequests": null,
            "MemoryReservation": 0,
            "MemorySwap": 0,
            "MemorySwappiness": null,
            "OomKillDisable": null,
            "PidsLimit": null,
            "Ulimits": null,
            "CpuCount": 0,
            "CpuPercent": 0,
            "IOMaximumIOps": 0,
            "IOMaximumBandwidth": 0,
            "Mounts": [
                {
                    "Type": "volume",
                    "Source": "sonia",
                    "Target": "/app"
                }
            ],
            "MaskedPaths": [
                "/proc/asound",
                "/proc/acpi",
                "/proc/kcore",
                "/proc/keys",
                "/proc/latency_stats",
                "/proc/timer_list",
                "/proc/timer_stats",
                "/proc/sched_debug",
                "/proc/scsi",
                "/sys/firmware",
                "/sys/devices/virtual/powercap"
            ],
            "ReadonlyPaths": [
                "/proc/bus",
                "/proc/fs",
                "/proc/irq",
                "/proc/sys",
                "/proc/sysrq-trigger"
            ]
        },
        "GraphDriver": {
            "Data": {
                "LowerDir": "/var/lib/docker/overlay2/a5d65246857c5321a5d668c87c253fb7a20dca3ead8cb89bdab0a59fee5e840d-init/diff:/var/lib/docker/overlay2/5588e4fac4150ae6ced29236202f90abc8394a8524670b900a2ef4863f7c6778/diff:/var/lib/docker/overlay2/c6e8ba30661f501fb91651212ae924b01d02fedd216ee254b70a789b008fdace/diff:/var/lib/docker/overlay2/19b39104f9cdcb4a39b9714b4acb4b14678f53d853c08668fd766370893fbc1d/diff:/var/lib/docker/overlay2/dd75f91c991a3173de2ce96b11a88bd496d37c943da459bb78d54bb24b9ffb20/diff:/var/lib/docker/overlay2/58379d92c8d6e138b932ceefba6dbbcddc3a17358e3b01f592b93e7821ddc33f/diff:/var/lib/docker/overlay2/82f15649a98533be88e451e3e40ac49bab584eb0812f83d66c23947f408f4417/diff:/var/lib/docker/overlay2/d10de84a98e10944cd5f45f818978da75679c854d833f4086015dae2f9031596/diff",
                "MergedDir": "/var/lib/docker/overlay2/a5d65246857c5321a5d668c87c253fb7a20dca3ead8cb89bdab0a59fee5e840d/merged",
                "UpperDir": "/var/lib/docker/overlay2/a5d65246857c5321a5d668c87c253fb7a20dca3ead8cb89bdab0a59fee5e840d/diff",
                "WorkDir": "/var/lib/docker/overlay2/a5d65246857c5321a5d668c87c253fb7a20dca3ead8cb89bdab0a59fee5e840d/work"
            },
            "Name": "overlay2"
        },
        "Mounts": [
            {
                "Type": "volume",
                "Name": "sonia",
                "Source": "/var/lib/docker/volumes/sonia/_data",
                "Destination": "/app",
                "Driver": "local",
                "Mode": "z",
                "RW": true,
                "Propagation": ""
            }
        ],
        "Config": {
            "Hostname": "120a02ba807f",
            "Domainname": "",
            "User": "",
            "AttachStdin": false,
            "AttachStdout": false,
            "AttachStderr": false,
            "ExposedPorts": {
                "80/tcp": {}
            },
            "Tty": false,
            "OpenStdin": false,
            "StdinOnce": false,
            "Env": [
                "PATH=/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin",
                "NGINX_VERSION=1.25.5",
                "NJS_VERSION=0.8.4",
                "PKG_RELEASE=1~bookworm"
            ],
            "Cmd": [
                "nginx",
                "-g",
                "daemon off;"
            ],
            "Image": "nginx:latest",
            "Volumes": null,
            "WorkingDir": "",
            "Entrypoint": [
                "/docker-entrypoint.sh"
            ],
            "OnBuild": null,
            "Labels": {
                "maintainer": "NGINX Docker Maintainers <docker-maint@nginx.com>"
            },
            "StopSignal": "SIGQUIT"
        },
        "NetworkSettings": {
            "Bridge": "",
            "SandboxID": "e0019f678a89a278575715489730b259d50c81639152166920bad106ceb8c1a1",
            "HairpinMode": false,
            "LinkLocalIPv6Address": "",
            "LinkLocalIPv6PrefixLen": 0,
            "Ports": {
                "80/tcp": null
            },
            "SandboxKey": "/var/run/docker/netns/e0019f678a89",
            "SecondaryIPAddresses": null,
            "SecondaryIPv6Addresses": null,
            "EndpointID": "c0153ca90d1bbdcfe6767cecec26f9d86d6e784b102f3beca31efe107fa77a86",
            "Gateway": "172.17.0.1",
            "GlobalIPv6Address": "",
            "GlobalIPv6PrefixLen": 0,
            "IPAddress": "172.17.0.2",
            "IPPrefixLen": 16,
            "IPv6Gateway": "",
            "MacAddress": "02:42:ac:11:00:02",
            "Networks": {
                "bridge": {
                    "IPAMConfig": null,
                    "Links": null,
                    "Aliases": null,
                    "NetworkID": "04e2ad48a568a9546703078a96eba7a3d5aae8c3676fac95c252ee631a6728ea",
                    "EndpointID": "c0153ca90d1bbdcfe6767cecec26f9d86d6e784b102f3beca31efe107fa77a86",
                    "Gateway": "172.17.0.1",
                    "IPAddress": "172.17.0.2",
                    "IPPrefixLen": 16,
                    "IPv6Gateway": "",
                    "GlobalIPv6Address": "",
                    "GlobalIPv6PrefixLen": 0,
                    "MacAddress": "02:42:ac:11:00:02",
                    "DriverOpts": null
                }
            }
        }
    }
]



Delete volume.....

docker volume rm sonia
Error response from daemon: remove sonia: volume is in use - [120a02ba807fff2e72a676a6623cb63a80bacd8d2ab0953cd59faad1a0f68394]

stop container/delete container then delete volume........

