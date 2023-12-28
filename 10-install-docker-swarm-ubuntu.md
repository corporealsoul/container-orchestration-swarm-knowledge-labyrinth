
### Master / Controller  Node,

https://docs.docker.com/engine/swarm/swarm-tutorial/create-swarm/

<br>

**Configure the Cluster hosts file,**

`[anup@rhel-92-04 ~]$ sudo nano /etc/hosts `

    192.168.56.4    rhel-92-04
    192.168.56.8    ubuntu-22042-08

<br>

**Disable firewall,**

`[anup@rhel-92-04 ~]$ sudo systemctl stop firewalld.service`

<br>

**Initialize the Swarm,**

`[anup@rhel-92-04 ~]$ docker swarm init --advertise-addr 192.168.56.4`

    Swarm initialized: current node (i793vqol6mo8wg1yysv7igsv0) is now a manager.

`[anup@rhel-92-04 ~]$ docker node ls`

<br>

**Test Docker Swarm Installation by Creating Services,**

`[anup@rhel-92-04 ~]$ sudo docker service create --name web-server --publish 8080:80 nginx:latest`

`[anup@rhel-92-04 ~]$ sudo docker service ls`


**http://192.168.56.4:8080/**

<br>

**Create replicas of the service,**

`[anup@rhel-92-04 ~]$ sudo docker service scale web-server=2`

`[anup@rhel-92-04 ~]$ sudo docker service ls`

<br>

### Worker node,

**Configure the Cluster hosts file,**

`anup@ubuntu-22042-08:~$ sudo nano /etc/hosts`

    192.168.56.4    rhel-92-04
    192.168.56.8    ubuntu-22042-08

<br>

**Join Master / Controller,**

`anup@ubuntu-22042-08:~$ docker swarm join --token SWMTKN-1-45x09d832qxhky145ntn0g65700upbrfmmte11dviui0rvj3cv-5t1f3hbjmy9swr6sv3vxmytw0 192.168.56.4:2377`

**http://192.168.56.8:8080/**

<br>
