# Docker Networking

Networking allows containers to communicate with each other and with the host system. Containers run isolated from the host system
and need a way to communicate with each other and with the host system.

By default, Docker provides two network drivers for you, the bridge and the overlay drivers. 

```
docker network ls
```

```
NETWORK ID          NAME                DRIVER
xxxxxxxxxxxx        none                null
xxxxxxxxxxxx        host                host
xxxxxxxxxxxx        bridge              bridge
```


### Bridge Networking

The default network mode in Docker. It creates a private network between the host and containers, allowing
containers to communicate with each other and with the host system.

![image](https://user-images.githubusercontent.com/43399466/217745543-f40e5614-ac34-4b78-85a9-91b24512388d.png)

If you want to secure your containers and isolate them from the default bridge network you can also create your own bridge network.

```
docker network create -d bridge my_bridge
```

Now, if you list the docker networks, you will see a new network.

```
docker network ls

NETWORK ID          NAME                DRIVER
xxxxxxxxxxxx        bridge              bridge
xxxxxxxxxxxx        my_bridge           bridge
xxxxxxxxxxxx        none                null
xxxxxxxxxxxx        host                host
```

This new network can be attached to the containers, when you run these containers.

```
docker run -d --net=my_bridge --name db training/postgres
```

This way, you can run multiple containers on a single host platform where one container is attached to the default network and 
the other is attached to the my_bridge network.

These containers are completely isolated with their private networks and cannot talk to each other.

![image](https://user-images.githubusercontent.com/43399466/217748680-8beefd0a-8181-4752-a098-a905ebed5d2a.png)


However, you can at any point of time, attach the first container to my_bridge network and enable communication

```
docker network connect my_bridge web
```

![image](https://user-images.githubusercontent.com/43399466/217748726-7bb347d0-3736-4f89-bdff-31d240b15150.png)


### Host Networking

This mode allows containers to share the host system's network stack, providing direct access to the host system's network.

To attach a host network to a Docker container, you can use the --network="host" option when running a docker run command. When you use this option, the container has access to the host's network stack, and shares the host's network namespace. This means that the container will use the same IP address and network configuration as the host.

Here's an example of how to run a Docker container with the host network:

```
docker run --network="host" <image_name> <command>
```

Keep in mind that when you use the host network, the container is less isolated from the host system, and has access to all of the host's network resources. This can be a security risk, so use the host network with caution.

Additionally, not all Docker image and command combinations are compatible with the host network, so it's important to check the image documentation or run the image with the --network="bridge" option (the default network mode) first to see if there are any compatibility issues.

### Overlay Networking

This mode enables communication between containers across multiple Docker host machines, allowing containers to be connected to a single network even when they are running on different hosts.

### Macvlan Networking

This mode allows a container to appear on the network as a physical host rather than as a container.

CLASS EXPLANATION
....................

VM = OS+ application
container = lightweighted without mini os less packages

subnet = networking group..

        TWO CASES...................

2 containers have to communicate frontend and backend....
(1) ASSOCIATION AND (front end and backend)
(2) LOGICAL ISOLATION  (login and finance containers)

eth0:192.16.3.4 network in host 
container app 172.17.0.2

separate networks

              networking error when conatiner ping to host

            docker created a virtualETH/ network ....[DOCKER 0].....
1. Bridge networking (default networking)
    OOTB networking can be solved.
   Docker allows to create custom bridge network......instead of going throigh same path we can split networks..
container 1 (login) Veth and Docker 0 
conatiner 2 (logout) veth and docker 0
container 3 (finance/payments)  secure  .....custom bridge network./virtual bridge network............using docker network command...
docker run --network



     DOCKER OFFERS MULTIPLE NETWORKING OPTIONS

     
3. HOST NETWORKING
    Docker will directly bind with eth0 of host...
    192.16.3.4
    192.16.3.6
    docker and host networking is same...problematic approach

    Container is secure in nature.....



4. OVERLAY NETWORKING (Conatiner orchestration engines)
   Kubernetes
   docker swarm

class for creating virtual eth0 and login/logout conatiners COMMANDS

   1  docker login
   2  docker run -d --name login nginx:latest
   3 docker exec -it login /bin/bash
   4  apt update
   5 apt-get install iputils-ping -y
   6 ping -V
     docker run -d --name logout nginx:latest
   7 docker ps
   8 docker inspect login
   9 docker inspect logout

       To show networks  host/login/logout
docker network ls
NETWORK ID     NAME      DRIVER    SCOPE
298b967d3bce   bridge    bridge    local
36783b67f808   host      host      local
81b0e6332829   none      null      local

      To remove networks
docker network rm test

creation of brige network
   docker network create secure-network
   docker network ls
   ETWORK ID     NAME             DRIVER    SCOPE
298b967d3bce   bridge           bridge    local
36783b67f808   host             host      local
81b0e6332829   none             null      local

          SECURE NETWORK
docker run -d --name finance  --network=secure-network  nginx:latest
docker ps
CONTAINER ID   IMAGE          COMMAND                  CREATED          STATUS          PORTS     NAMES
2b0282f8c652   nginx:latest   "/docker-entrypoint.…"   17 seconds ago   Up 16 seconds   80/tcp    finance
60133b63239d   nginx:latest   "/docker-entrypoint.…"   17 minutes ago   Up 17 minutes   80/tcp    logout
73c34c909c1b   nginx:latest   "/docker-entrypoint.…"   36 minutes ago   Up 35 minutes   80/tcp    login

          HOST NETWORKING
$ docker run -d --name host-demo --network=host  nginx:latest
ONTAINER ID   IMAGE          COMMAND                  CREATED          STATUS          PORTS     NAMES
d73c1d6a7bc1   nginx:latest   "/docker-entrypoint.…"   4 seconds ago    Up 3 seconds              host-demo
2b0282f8c652   nginx:latest   "/docker-entrypoint.…"   4 minutes ago    Up 4 minutes    80/tcp    finance
60133b63239d   nginx:latest   "/docker-entrypoint.…"   21 minutes ago   Up 21 minutes   80/tcp    logout
73c34c909c1b   nginx:latest   "/docker-entrypoint.…"   40 minutes ago   Up 40 minutes   80/tcp    login

DOCKER DIDNTOT CREATE ANY VIRTUAL NETWORK..DIRECTLY BIND WITH HOST NETWORKING

   same docker 0 then common path for hacker.....out of the BOX  [00TB] bridge networking........V(eth) 


              docker inspect host-demo
              
   works": {
                "host": {
                    "IPAMConfig": null,
                    "Links": null,
                    "Aliases": null,
                    "NetworkID": "36783b67f808d22aafc2c3fa32d482e9cb4626feb00ce9645fd717097b42b911",
                    "EndpointID": "24c0248ab4fdf32aeae03ce597ed7c4684f17dbe26912a466976513e51c88ee6",
                    "Gateway": "",
                    "IPAddress": "",
                    "IPPrefixLen": 0,
                    "IPv6Gateway": "",
                    "GlobalIPv6Address": "",
                    "GlobalIPv6PrefixLen": 0,
                    "MacAddress": "",
                    "DriverOpts": null
                }
   

