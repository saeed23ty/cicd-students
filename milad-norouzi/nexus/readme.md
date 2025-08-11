Install docker and docker compose(َUse Install_docker.sh) to install docker

Install nexus registry with docker and docker compose

```bash
sudo docker compose up -d
```

Run command on server

```
chown -R 200:200 /data/registry/
chown -R 200:200 /data/registry/nexus-data
```

admin password is:

```
docker exec -it nexus cat /nexus-data/admin.password
```

### Install nginx

```bash
sudo apt-get update
sudo apt-get install nginx
```

Copy `nexus` and `docker` file to `/etc/nginx/site-avalible`

sudo apt-get install python3-certbot-ngin nginx
certbot --nginx -d YOUR_DOMAIN

## For wildcard run:

```bash
sudo apt-get install certbot
sudo apt-get install python3-certbot-nginx
sudo certbot certonly --manual --preferred-challenges=dns --server https://acme-v02.api.letsencrypt.org/directory --manual-public-ip-logging-ok -d "*.YOUR_DOMAIN"
```

### Create nginx config files

```
ln -s /etc/nginx/sites-available/nexus /etc/nginx/sites-enabled/
ln -s /etc/nginx/sites-available/docker /etc/nginx/sites-enabled/
unlink /etc/nginx/sites-enabled/default
```

### Test nginx config and reload

```bash
sudo nginx -t
sudo nginx -s reload
sudo systemctl restart nginx
```

### Open browser and test nexus and docker registry

https://registry.anisa.local

### Login to docker registry in your cli

```bash
docker login docker.anisa.local
```

If you get bellow error it's because of HTTPS

```bash
Error response from daemon: Get "https://docker.anisa.local/v2/": http: server gave HTTP response to HTTPS client
```

You should add insecure registry in your docker config

**Make sure you add it to all docker hosts that you want to use this registry**

```bash
sudo vim /etc/docker/daemon.json

{
    "insecure-registries": ["docker.anisa.local"]
}
```

Restart docker service

```bash
sudo systemctl restart docker
sudo systemctl status docker
```
