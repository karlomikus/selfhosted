# My LAN selfhosted apps

## Hardware

- Raspberry Pi 3
- Asus RT-AX58U (with Merlin WRT)

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

### Accessing services via .local domains

You need DNS for this to work. Since I'm using adguard as my DNS, I can add DNS rewrites.

- Go to you adguard instance > Filters > DNS Rewrites
- Add DNS rewrite, use your server IP withour port for IP address

To access home assistant via reverse proxy you [need additional configuration](https://www.home-assistant.io/integrations/http#reverse-proxies).

### Setup network

Configure your router to work with adguard [following this guide](https://www.reddit.com/r/pihole/comments/dfm5j4/guide_for_asuswrtmerlin_users_with_screenshots/).

## Todo
- setup vpn (blocked by ISP router unable to switch to bridge mode)
- ~~fix permissions~~
- ~~remove privileged~~
- ~~setup container reverse proxy~~
- ~~custom domains (via dnsmasq/adguard)~~

## Services
- Jellyfin for media center
- Home Assistant for smart home devices
- Adguard for network wide adblock
- Cockpit for monitoring
- Portainer for container management
- Traefik for reverse proxy
- [TODO] Paperless-NGX for document management
- [TODO] Authelia for service authentication
- [TODO] Nextcloud for personal cloud
