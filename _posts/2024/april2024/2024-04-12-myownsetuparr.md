---
title: Own Arr Media
date: 2024-04-12 11:20 +500
categories: [homelab, own, arr]
tags: [homarr,sonarr,prowlarr,flaresolverr,jellyfin,transmission,filebrowser]
---

## New Setup

```bash
ip a
```
Note down local/internal IP address.

## Copy below to do magic

```
mkdir -p /data/media/tv /data/media/music /data/media/movies /data/torrents/tv /data/torrents/music /data/torrents/movies arr
chown -R $USER:$USER /data
chmod -R 777 /data
cd arr
nano docker-compose.yml
```
> Now Paste the yaml file below in nano (docker-compose.yml) and save it by **ctrl+x** **Y** **Press Enter**
{: .prompt-tip }

## The yaml ARR

```yaml
---
services:
  sonarr:
    container_name: sonarr
    image: linuxserver/sonarr:latest
    restart: unless-stopped
    ports:
      - 8989:8989
    environment:
      - PUID=1000
      - PGID=1000
      - TZ=Europe/Stockholm
    volumes:
      - ./sonarr:/config
      - /data:/data
  radarr:
    container_name: radarr
    image: linuxserver/radarr:latest
    restart: unless-stopped
    ports:
      - 7878:7878
    environment:
      - PUID=1000
      - PGID=1000
      - TZ=Europe/Stockholm
    volumes:
      - ./radarr:/config
      - /data:/data
  lidarr:
    container_name: lidarr
    image: linuxserver/lidarr:latest
    restart: unless-stopped
    ports:
      - 8686:8686
    environment:
      - PUID=1000
      - PGID=1000
      - TZ=Europe/Stockholm
    volumes:
      - ./lidarr:/config
      - /data:/data
  prowlarr:
    container_name: prowlarr
    image: lscr.io/linuxserver/prowlarr:latest
    restart: unless-stopped
    ports:
      - 9696:9696
    environment:
      - PUID=1000
      - PGID=1000
      - TZ=Europe/Stockholm
    volumes:
      - ./prowlarr:/config
  jellyseerr:
    container_name: jellyseerr
    image: fallenbagel/jellyseerr:latest
    restart: unless-stopped
    ports:
      - 5055:5055
    environment:
      - PUID=1000
      - PGID=1000
      - TZ=Europe/Stockholm 
    volumes:
      - ./jellyseerr:/config
  flaresolverr:
    container_name: flaresolverr
    image: ghcr.io/flaresolverr/flaresolverr:latest
    restart: unless-stopped
    ports:
      - 8191:8191
    environment:
      - LOG_LEVEL=${LOG_LEVEL:-info}
      - LOG_HTML=${LOG_HTML:-false}
      - CAPTCHA_SOLVER=${CAPTCHA_SOLVER:-none}
      - PUID=1000
      - PGID=1000
      - TZ=Europe/Stockholm
    volumes:
      - ./flaresolverr:/config
  jellyfin:
    container_name: jellyfin
    image: linuxserver/jellyfin:latest
    restart: unless-stopped
    ports:
      - 8096:8096
    environment:
      - PUID=1000
      - PGID=1000
      - TZ=Europe/Stockholm
    volumes:
      - ./jellyfin:/config
      - /data/media:/data/media
  transmission:
    container_name: transmission
    image: linuxserver/transmission:latest
    restart: unless-stopped
    ports:
      - 9091:9091
      - 51413:51413
      - 51413:51413/udp
    environment:
      - PUID=1000
      - PGID=1000
      - TZ=Europe/Stockholm
    volumes:
      - ./transmission:/config
      - /data/torrents:/data/torrents:rw
  ytdl_material:
      environment: 
          ytdl_mongodb_connection_string: 'mongodb://ytdl-mongo-db:27017'
          ytdl_use_local_db: 'false'
          write_ytdl_config: 'true'
      restart: unless-stopped
      depends_on:
          - ytdl-mongo-db
      volumes:
          - ./ytdl/appdata:/app/appdata
          - /data/media/ytdl/audio:/app/audio
          - /data/media/ytdl/video:/app/video
          - /data/media/ytdl/subscriptions:/app/subscriptions
          - /data/media/ytdl/users:/app/users
      ports:
          - 8998:17442
      image: tzahi12345/youtubedl-material:latest
  ytdl-mongo-db:
      image: mongo:4
      logging:
          driver: none          
      container_name: mongo-db
      restart: unless-stopped
      volumes:
          - ./ytdl/db/:/data/db
  filebrowser:
    container_name: filebrowser
    image: filebrowser/filebrowser:latest
    restart: unless-stopped
    ports:
      - 8080:80
    environment:
      - PUID=1000
      - PGID=1000
      - TZ=Europe/Stockholm
      - FB_NOAUTH=true
    volumes:
      - ./filebrowser:/config
      - /:/srv
  homarr:
    container_name: homarr
    image: ghcr.io/ajnart/homarr:latest
    restart: unless-stopped
    ports:
      - 80:7575
    environment:
      - PUID=1000
      - PGID=1000
      - TZ=Europe/Stockholm
    volumes:
      - /var/run/docker.sock:/var/run/docker.sock
      - ./homarr/configs:/app/data/configs
      - ./homarr/icons:/app/public/icons
      - ./homarr/data:/data
  watchtower:
    container_name: watchtower
    image: containrrr/watchtower
    volumes:
      - /var/run/docker.sock:/var/run/docker.sock
    environment:
      - PUID=1000
      - PGID=1000
      - TZ=Europe/Stockholm
      - WATCHTOWER_CLEANUP=true
      - WATCHTOWER_POLL_INTERVAL=604800
```

## Run it 

```bash
docker compose up -d
```
After it is done just go the local ip of the server and configure Homarr(homepage) with links to easily configure rest of the services and conbine them together

## Ports

* Homarr = IP:80
* Sonarr = IP:8989
* Radarr = IP:7878
* Lidarr = IP:8686
* Prowlarr = IP:9696
* Jellyseerr = IP:5055
* Flaresolverr = IP:8191
* Jellyfin = IP:8096
* Transmission = IP:9091
* YoutubeDownload = IP:8998
* FileBrowser = IP:8080