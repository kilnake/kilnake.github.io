---
title: Scripted Media Setup
date: 2024-04-30 16:44 +500
categories: [homelab, mediascript]
tags: [mediascript]
pin: false
---

## Final script

>

```bash
bash -c "$(wget -qO - https://raw.githubusercontent.com/kilnake/proxmox/main/auto.sh)"
```

{: .prompt-tip }

## This is content of the script

```bash
#!/bin/sh

mkdir -p /data/media/tv /data/media/music /data/media/movies /data/torrents/tv /data/torrents/music /data/torrents/movies /arr
chown -R $USER:$USER /data /arr
chmod -R 755 /data /arr
cd /arr
wget -q -O docker-compose.yml https://raw.githubusercontent.com/kilnake/proxmox/main/docker-compose.yml
docker compose up -d
ip -4 address show dev eth0
```

## Content of docker-compose.yml

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
  watcharr:
    container_name: watcharr
    image: ghcr.io/sbondco/watcharr:latest
    restart: unless-stopped
    ports:
      - 3080:3080
    environment:
      - PUID=1000
      - PGID=1000
      - TZ=Europe/Stockholm
    volumes:
      - ./watcharr/data:/data
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
      - ./jellyseerr:/app/config
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
  navidrome:
    container_name: navidrome
    image: deluan/navidrome:latest
    restart: unless-stopped
    ports:
      - 4533:4533
    environment:
      - PUID=1000
      - PGID=1000
      - TZ=Europe/Stockholm
    volumes:
      - ./navidrome:/config
      - ./navidrome/data:/data
      - /data/media/music:/data/media/music:ro
  #  nginx:
  #    container_name: nginxformedia
  #   image: nginx:latest
  #    ports:
  #      - "9999:80"
  #    volumes:
  #     - ./nginxformedia:/config
  #      - ./nginx.conf:/etc/nginx/nginx.conf:ro
  #     - /data/media:/data/media:ro
  #   restart: unless-stopped
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
      ytdl_mongodb_connection_string: "mongodb://ytdl-mongo-db:27017"
      ytdl_use_local_db: "false"
      write_ytdl_config: "true"
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
