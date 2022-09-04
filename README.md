# selfhosted

todo:
- fix permissions
- remove privileged
- setup vpn

# misc

- run portainer

`docker run -d -p 8000:8000 -p 9443:9443 --name=portainer --restart=always -v /var/run/docker.sock:/var/run/docker.sock -v portainer_data:/data portainer/portainer-ce:latest`

- fix pihole / network bullshit

`sudo ip route add default via 192.168.50.1`

- monitoring

Use cockpit project, available at port <hostname>:9090

```
$ sudo apt install cockpit
$ sudo systemctl start cockpit
```
