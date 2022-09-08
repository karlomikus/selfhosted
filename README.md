# My LAN selfhosted apps

## Hardware

- Raspberry Pi 3
- Asus RT-AX58U

## Setup

### Mount media folder

I use windows share from my PC. Enable share on a folder you want and mount it on server

``` bash
$ sudo mkdir /mnt/share
$ sudo mount -t cifs -o username=Guest //<PC-IP>/SharedFolder /mnt/share
```

Add mount to fstab to automatically mount on restarts

``` bash
$ sudo vim /etc/fstab
```

Add the following line:

```
//<PC-IP>/SharedFolder    /mnt/share    cifs    username=Guest,password=    0    0
```

### Run containers

Create a new network

``` bash
$ docker network create web-proxy
```

Pull repo somewhere in home folder and run

``` bash
$ docker compose up -d
```

(optional) Setup portainer

``` bash
$ docker run -d -p 8000:8000 -p 9443:9443 --name=portainer --restart=always -v /var/run/docker.sock:/var/run/docker.sock -v portainer_data:/data portainer/portainer-ce:latest
```

### Setup monitoring

Use cockpit project, available at port `<hostname>:9090`

``` bash
$ sudo apt install cockpit
$ sudo systemctl start cockpit
```

## Todo
- ~~fix permissions~~
- ~~remove privileged~~
- setup vpn
- setup container reverse proxy
- custom domains (via dnsmasq/adguard)
