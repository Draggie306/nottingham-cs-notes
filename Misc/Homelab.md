
# Cheat Sheet

### Known Issues

#### OOM/system freezes:

```sh
draggie@rpi:~ $  journalctl -p err -b

Nov 25 13:55:16 rpi systemd[1]: systemd-journald.service: Watchdog timeout (limit 3min)!
Nov 25 18:14:16 rpi kernel: Out of memory: Killed process 1406387 (ffmpeg) total-vm:4514288kB, anon-rss:2414912kB, file-rss:0kB, shmem-rss:0kB, UID:0 pgtables:2096 oom_score_adj:0
```

```
draggie@rpi:~ $ dmesg | egrep -i "error|sdhci|mmc|timeout|I/O"

[86409.553009] systemd[1]: systemd-journald.service: Failed with result 'timeout'.
```


## Docker
- Update all containers in current directory with docker compose:
	- `sudo docker compose pull && docker compose up -d`
- Restart containers in current directory with docker compose:
	- ``docker compose down && docker compose up -d`
- Get latest 10 log entries in current directory:
	- `docker compose logs | tail`
- Get all container status system-wide
	- `docker ps`
- Prune all unused images in the last 24 hours
	- `docker image prune -a --filter "until=24h"`

Settings:
- Container/image data root is located on the external SSD to prevent extra SD card wear and to improve speed

Located at `/etc/docker/daemon.json`:
```json
{
	"min-api-version": "1.41",
	"data-root": "/mnt/ssd1/docker"
}
```

**TODO: Temporary change due to a Portainer bug. When updating Portainer, refer to this issue.**
- https://github.com/portainer/portainer/issues/12925#issuecomment-3560758801



## Misc Tools
- Get hard drive temperatures:
	- `sudo smartctl -a /dev/sdb | grep "194"`
	- `sudo smartctl -a /dev/sdb` *(all SMART data)*

## System
### Commands
- Reboot
	- `sudo reboot`
- Update all packages system-wide:
	- `sudo apt-get update && sudo apt-get upgrade --autoremove -y`
- Current usage/task manager
	- `htop`
	- Normal mem usage: 4-5G/7.87G (Swap usage often gets to 2gb, with default swappiness, do not worry.)

### Configs
- Fstab entries `sudo nano /etc/fstab`
	- SSD Cache (usb3->sata) (256gb) `UUID=d6ecfcd5-2703-41bf-9301-10c403b6fb0c /mnt/ssd1 ext4 nofail,defaults 0 2`
	- External 20tb drive (usb3) `UUID=302749e2-3434-4b3f-b3b8-d36a7df58ac0 /mnt/mega ext4 nofail,defaults 0 2`
- Swapfile/ram config: `sudo nano /etc/dphsys-swapfile`
	- `CONF_SWAPFILE=/mnt/ssd1/swap`
	- `CONF_SWAPSIZE=2048`
- Swappiness config: `sudo nano /etc/sysctl.conf`, at the bottom:
	- `vm.swappiness = 10`
		- Else, the swap eventually fills up with data while ram is left over.
		- *2025-12-25: set swappiness to 10 from previous value 15. Testing if this reduces swap usage more.*
	- apply with `sudo sysctl -p`


# Services: Docker, containerised

## arr stack
*For: Media management/downloads, music, streaming, TV* 

Location: `services/arr/
Restart: `docker compose down && docker compose up -d`


### qBittorrent 

Access qBittorrent at http://192.168.1.3:9665/

Restraints: qBittorrent depends on Gluetun. Gluetun connects via PIA VPN with portforwarding enabled.

**Issues**: not downloading? Go to **Tools -> Options -> Advanced** and check **Optional IP address to bind to** is set to the present IPv4 address, e.g. 10.24.110.35, and not blank/any, and scroll to the bottom -> **Save**. (Network interface should be `tun0`.)

### Gluetun

Check logs with `docker logs gluetun | tail`

Depends on: internet access to `ibaguette.com`

![[Pasted image 20251106001330.png]]

```yaml
  gluetun:
    image: qmcgaw/gluetun:latest
    container_name: gluetun
    restart: unless-stopped
    cap_add:
      - NET_ADMIN
    devices:
      - /dev/net/tun:/dev/net/tun
    volumes:
      - ./config/gluetun:/gluetun
    environment:
      - VPN_SERVICE_PROVIDER=${VPN_SERVICE_PROVIDER}
      - OPENVPN_USER=${VPN_USER}
      - OPENVPN_PASSWORD=${VPN_PASS}
      - SERVER_REGIONS=${SERVER_REGIONS}
      - TZ=${TZ}
      - VPN_PORT_FORWARDING=on
      - DOT=off
      - DNS_ADDRESS=1.1.1.1
      - VPN_INTERFACE=tun0

    ports:
      - 10101:8000 # expose 10101
      - 9665:9665   # qBittorrent WebUI
#      - 9696:9696 # prowlarr
#      - 25505:25505   # Torrent TCP
#      - 25505:25505/udp # Torrent UDP
#    healthcheck:
#      test: ["CMD", "wget", "--spider", "http://google.com"]
#      interval: 30s
#      timeout: 10s
#      retries: 5
    healthcheck:
      test: ping -c 1 ibaguette.com || exit 1
      interval: 20s
      timeout: 10s
      retries: 5
#    restart: unless-stopped
```


### Sonarr
Access: http://192.168.1.3:8989/  
Purpose: TV series management & episode automation.  
Depends on: qBittorrent, Prowlarr.  

### Radarr  
Access: http://192.168.1.3:7878/  
Purpose: Movie management & automation.  
Depends on: qBittorrent, Prowlarr.  

### Bazarr  
Access: http://192.168.1.3:6767/  
Purpose: Subtitle downloads & sync.  
Depends on: Sonarr, Radarr.  

### Prowlarr  
Access: http://192.168.1.3:9696/  
Location: `services/arr/prowlarr/`  
Purpose: Indexer management (feeds Sonarr/Radarr).

### Jellyseerr  
Access: http://192.168.1.3:5055/  
Purpose: Request & manage media through Jellyfin.  
Depends on: Jellyfin, Radarr, Sonarr.  

---

## Jellyfin  
Purpose: Media server & streaming frontend.  

Location: `services/jellyfin/`  
Restart: `docker compose restart`  

Access: http://192.168.1.3:8096/  

External access: https://j.oling.dev (Cloudflare Tunnel) (**J**ellyfin)


---

## Immich Stack  
*For: Self-hosted photo/video backup & AI tagging*  

Location: `services/immich-app/`  
Restart: `docker compose down && docker compose up -d`  

Notes:
- Immich app's `thumbs`, the `postgres` database, `backups`, `profile` and `upload` temp cache directories are located on the SSD cache at `/mnt/ssd1/immich-cache`. The `library` and `encoded-video` are on `/mnt/mega/immich/library`


`.env` config (secrets removed):
```yml
# The location where your uploaded files are stored
UPLOAD_LOCATION=/mnt/mega/immich/library/
# The location where your database files are stored
DB_DATA_LOCATION=/mnt/ssd1/immich-cache/postgres/postgres/

# The Immich version to use. You can pin this to a specific version like "v1.71.0"
IMMICH_VERSION=release

# Connection secret for postgres. You should change it to a random password
DB_PASSWORD=<Check Bitwarden>

# Remote Transcoding: Add api worker
# IMMICH_WORKERS_INCLUDE: 'api'
# -- End remote transcoding -- 

###################################################################################
# Upload File Location
#
# This is the location where uploaded files are stored.
###################################################################################

THUMBS_LOCATION=/mnt/ssd1/immich-cache/thumbs/
PROFILE_LOCATION=/mnt/ssd1/immich-cache/profile/
BACKUP_LOCATION=/mnt/ssd1/immich-cache/backups/
```

docker-compose.yml
```yml
name: immich

services:
  immich-server:
    container_name: immich_server
#    image: ghcr.io/immich-app/immich-server:1.132.3
    image: ghcr.io/immich-app/immich-server:${IMMICH_VERSION:-release}
    # extends:
    #   file: hwaccel.transcoding.yml
    #   service: cpu # set to one of [nvenc, quicksync, rkmpp, vaapi, vaapi-wsl] for accelerated transcoding
    volumes:
      # Do not edit the next line. If you want to change the media storage location on your system, edit the value of UPLOAD_LOCATION in the .env file
      - ${UPLOAD_LOCATION}:/usr/src/app/upload
      - /etc/localtime:/etc/localtime:ro
      - /mnt/mega/Immich-Takeout-Test/:/mnt/mega/Immich-Takeout-Test
      - ${THUMBS_LOCATION}:/usr/src/app/upload/thumbs
      - ${PROFILE_LOCATION}:/usr/src/app/upload/profile
    env_file:
      - .env
    ports:
      - '2283:2283'
    depends_on:
      - redis
      - database
    restart: always
    healthcheck:
      disable: false
    labels:
      - "com.centurylinklabs.watchtower.enable=false"

# DISABLE THIS to prevent unnecessary memory/loading (the model is only loaded for 5 minutes when requested, but still). It is about 20x faster to configure this to run remotely. No config change is needed within Immich itself if this is updated

#  immich-machine-learning:
#    container_name: immich_machine_learning
    # For hardware acceleration, add one of -[armnn, cuda, openvino] to the image tag.
    # Example tag: ${IMMICH_VERSION:-release}-cuda
#    image: ghcr.io/immich-app/immich-machine-learning:${IMMICH_VERSION:-release}
#    # extends: # uncomment this section for hardware acceleration - see https://immich.app/docs/features/ml-hardware-acceleration
#    #   file: hwaccel.ml.yml
#    #   service: cpu # set to one of [armnn, cuda, openvino, openvino-wsl] for accelerated inference - use the `-wsl` version for WSL2 where applicable
#    volumes:
#      - model-cache:/cache
#    env_file:
#      - .env
#    restart: always
#    healthcheck:
#      disable: false
#    ports:
#      - 3003:3003

  redis:
    container_name: immich_redis
    image: docker.io/redis:6.2-alpine@sha256:eaba718fecd1196d88533de7ba49bf903ad33664a92debb24660a922ecd9cac8
    healthcheck:
      test: redis-cli ping || exit 1
    labels:
      - "com.centurylinklabs.watchtower.enable=false"
    restart: always
    
    # Remote Transcoding: Expose redis
    # ports:
    #  - 6379:6379
    # -- End remote transcoding -- 


  database:
    container_name: immich_postgres
    image: ghcr.io/immich-app/postgres:14-vectorchord0.3.0-pgvectors0.2.0
    environment:
      POSTGRES_PASSWORD: ${DB_PASSWORD}
      POSTGRES_USER: ${DB_USERNAME}
      POSTGRES_DB: ${DB_DATABASE_NAME}
      POSTGRES_INITDB_ARGS: '--data-checksums'
      # Uncomment the DB_STORAGE_TYPE: 'HDD' var if your database isn't stored on SSDs
      # DB_STORAGE_TYPE: 'HDD'
    volumes:
      # Do not edit the next line. If you want to change the database storage location on your system, edit the value of DB_DATA_LOCATION in the .env file
      - ${DB_DATA_LOCATION}:/var/lib/postgresql/data
    restart: always

    # Remote Transcoding: Expose database
    # ports:
    #  - 5432:5432
    # -- End remote transcoding --

volumes:
  model-cache:
```

### Immich Server  
Access: http://192.168.1.3:2283/  
Purpose: API & backend for Immich app.

External access: https://p.oling.dev (Cloudflare Tunnel) (**P**hotos)

### Immich Machine Learning  
Access: http://192.168.1.3:3003/  
Purpose: Handles face recognition, object tagging, and clustering.  

- Note: Immich ML is set to be offloaded to the PC's 4070 super via remote ML, but gracefully falls back
#### Remote ML from Eduroam/uni networks

Eduroam blocks HTTP3/QUIC dialing that is required by Cloudflare Tunnels (and obviously, port forwarding is unavailable). To solve this:
- Run the cloudflared tunnel Docker run script and append `--protocol http2` to the command. This will look something like `docker run cloudflare/cloudflared:latest tunnel --no-autoupdate run --token xxx --protocol http2`
- The immich-ml container typically runs on port 3003. To expose this port from the host machine, but from within the Cloudflared container, in the Cloudflare Zero Trust dashboard, set the host to be `http://` `host.docker.internal:3003`.
- The terminal output should show something like: 
	- `2025-11-15T20:37:56Z INF Registered tunnel connection connIndex=0 connection=xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxx event=0 ip=198.41.192.7 location=lhr16 protocol=http2`
	- `2025-11-15T20:40:40Z INF Updated to new configuration config="{\"ingress\":[{\"hostname\":\"ai.oling.dev\",\"originRequest\":{},\"service\":\"http://host.docker.internal:3003\"},{\"service\":\"http_status:404\"}],\"warp-routing\":{\"enabled\":false}}" version=2`


### Immich Postgres  
Access: Internal only (5432).  
Purpose: Database for metadata & users.  

### Immich Redis  
Access: Internal only (6379).  
Purpose: Queue & caching layer.  

---

## Dawarich Stack  
*For: App hosting with Redis and PostgreSQL backend*  

Location: `services/dawarich/`  
Restart: `docker compose restart`  

### Dawarich App  
Access: http://192.168.1.3:3246/  
Purpose: Location history database
Depends on: Dawarich Sidekiq, Dawarich DB, Dawarich Redis.  
External access: https://l.oling.dev (Cloudflare Tunnel) (**L**ocation)
### Dawarich Sidekiq  
Access: Internal only.  
Purpose: Background jobs, async tasks.  

### Dawarich DB  
Access: Internal (5432).  
Purpose: PostgreSQL database for app data.  

### Dawarich Redis  
Access: Internal (6379).  
Purpose: Caching & queue management.  

---

## Paperless Stack  
*For: Document digitisation and management*  

Location: `services/paperless/`  
Restart: `docker compose down && docker compose up -d`  

### Paperless Webserver  
Access: http://192.168.1.3:8010/  

External access: https://d.oling.dev/dashboard (Cloudflare Tunnel) (**D**ocuments)

Purpose: Main web UI for managing scanned docs.  

### Paperless Broker (Redis)  
Access: Internal (6379).  
Purpose: Task broker for async processing.  

---

## Vaultwarden  
*For: Self-hosted password management*  

Location: `services/vaultwarden/`  
Restart: `docker compose restart`  

Access: http://192.168.1.3:34567/  

External access: https://vw.oling.dev (Cloudflare Tunnel) (**V**ault**w**arden)

- Data location `/home/draggie/services/vaultwarden/vw-data-new:/data`

---

## Network & Monitoring
*For: Network control, dashboards, uptime, and utilities*  

Location: `services/network/`  
Restart: `docker compose down && docker compose up -d`  

### Unifi Controller  
Access: https://192.168.1.3:8443/  
Purpose: Manages the Ubiquiti Unifi access points in the house for seamless roaming, stats etc.,  

### Homepage  
Access: http://192.168.1.3:3000/  
Purpose: Self-hosted dashboard for all services.  

### MySpeed  
Access: http://192.168.1.3:5216/  
Purpose: Internet speed testing & monitoring.  

Automations: 
- This sends a message to the Discord server via webhooks for every speed test. 
- Speedtests are ran according to schedule: `0,30 0-7 * * *`

### Portainer  
Access: https://192.168.1.3:9443/  
Purpose: Docker container management UI.  

### Uptime Kuma  
Access: http://192.168.1.3:3001/  
Purpose: Uptime monitoring dashboard.  

External access: https://s.oling.dev (Cloudflare Tunnel) (**S**tatus)

### Anisette-V3  
Access: http://192.168.1.3:6969/  
Purpose: Fake Apple ID server for sign-in/token services.  

External access: https://a.oling.dev/ (Cloudflare Tunnel) (**A**pple)

### MinMaxOctopusBot  
Access: Internal only.
Purpose: Octopus energy automatic tariff switcher.
Logs: `docker logs MinMaxOctopusBot | tail`

Automation:
- Runs every night at 23:00

Documentation:
- https://github.com/eelmafia/octopus-minmax

### Wakapi  
Access: https://c.oling.dev
Purpose: Code time tracker for me + invite-only uni friends.

Location: `services/wakapi/`  
Restart: `docker compose restart`  

Documentation: https://github.com/muety/wakapi

External access: https://c.oling.dev (Cloudflare Tunnel) (**C**ode)


---

# Services: Non-containerised

## Network
### Pi-hole
Access: http://192.168.1.3/admin
Purpose: Assign DHCP addresses to all devices on the network and act as an authoritative DNS server for each that can block ads and malicious 



## Radio



### welle-CLI
Required to receive DAB/DAB+ streams.

Multiplex block for talkSPORT: 11D
Search for all broadcasting from 11D: `welle-cli -c 11D`, output example:

Link to Icecast forwarding: `https://community.home-assistant.io/t/icecast-an-oldschool-and-audio-specific-complement-to-ha/325680/4`

Start webserver for multiplex block (connect at http://192.168.1.3:9876/)
`welle-cli -c 11D -w 9876`

```sh
nsemble label: D1 National     
Service list
  [0xc4cd] Radio X           [component 0 ASCTy: DAB+ ] [subch 17 bitrate:40 at SAd:330]
  [0xcae9] Heart  70s        [component 0 ASCTy: DAB+ ] [subch 19 bitrate:32 at SAd:306]
  [0xc0c0] talkSPORT         [component 0 ASCTy: DAB ] [subch 2 bitrate:64 at SAd:0]
MP2Decoder: using decoder 'NEON64'.
  [0xcee8] Gold Radio UK     [component 0 ASCTy: DAB+ ] [subch 8 bitrate:40 at SAd:156]
  [0xcfd1] Heart UK          [component 0 ASCTy: DAB+ ] [subch 5 bitrate:40 at SAd:96]
  [0xc1dc] Heart  80s        [component 0 ASCTy: DAB+ ] [subch 14 bitrate:40 at SAd:216]
  [0xc4f0] GB News Radio     [component 0 ASCTy: DAB+ ] [subch 24 bitrate:24 at SAd:486]
  [0xc9ed] Capital DANCE     [component 0 ASCTy: DAB+ ] [subch 23 bitrate:40 at SAd:438]
  [0xc246] Hits Radio 00s    [component 0 ASCTy: DAB+ ] [subch 32 bitrate:40 at SAd:828]
  [0xc0c2] LBC               [component 0 ASCTy: DAB ] [subch 15 bitrate:64 at SAd:48]
MP2Decoder: using decoder 'NEON64'.
  [0xc244] Grt Hits Rad 80s  [component 0 ASCTy: DAB+ ] [subch 30 bitrate:32 at SAd:744]
  [0xc243] Grt Hits Rad 70s  [component 0 ASCTy: DAB+ ] [subch 29 bitrate:32 at SAd:720]
  [0xc2a1] Classic FM        [component 0 ASCTy: DAB+ ] [subch 28 bitrate:64 at SAd:558]
  [0xcfe8] Heart Dance       [component 0 ASCTy: DAB+ ] [subch 4 bitrate:40 at SAd:186]
  [0xc8ea] LBC News          [component 0 ASCTy: DAB+ ] [subch 21 bitrate:32 at SAd:360]
  [0xc0c6] Magic Radio       [component 0 ASCTy: DAB+ ] [subch 11 bitrate:40 at SAd:690]
  [0xc5c0] KISS              [component 0 ASCTy: DAB+ ] [subch 10 bitrate:40 at SAd:660]
  [0xc245] Hits Radio 90s    [component 0 ASCTy: DAB+ ] [subch 31 bitrate:40 at SAd:768]
  [0xc4fb] Smooth Relax      [component 0 ASCTy: DAB+ ] [subch 27 bitrate:32 at SAd:606]
  [0xc9eb] Smooth Chill      [component 0 ASCTy: DAB+ ] [subch 12 bitrate:32 at SAd:414]
  [0xc4ca] UCB 1             [component 0 ASCTy: DAB+ ] [subch 7 bitrate:24 at SAd:468]
  [0xc9f3] Heart 00s         [component 0 ASCTy: DAB+ ] [subch 20 bitrate:40 at SAd:528]
  [0xcbe9] Heart  90s        [component 0 ASCTy: DAB+ ] [subch 18 bitrate:40 at SAd:246]
  [0xcbd8] UCB 2             [component 0 ASCTy: DAB+ ] [subch 9 bitrate:32 at SAd:504]
  [0xc6c0] Smooth UK         [component 0 ASCTy: DAB+ ] [subch 6 bitrate:40 at SAd:126]
  [0xc5da] Capital UK        [component 0 ASCTy: DAB+ ] [subch 22 bitrate:40 at SAd:384]
  [0xcfe6] KISSTORY          [component 0 ASCTy: DAB+ ] [subch 13 bitrate:40 at SAd:798]
  [0xc1c0] Absolute Radio    [component 0 ASCTy: DAB+ ] [subch 3 bitrate:40 at SAd:630]
  [0xc37b] Capital XTRA      [component 0 ASCTy: DAB+ ] [subch 16 bitrate:40 at SAd:276]
**** Enter '.' to quit.
{"UTCTime":{"day":2,"hour":21,"minutes":50,"month":1,"seconds":45,"year":2026}}
[0xc0c2] rate 24000 mode MPEG 2.0 Layer II, 24 kHz Mono @ 64 kbit/s
[0xc0c0] rate 24000 mode MPEG 2.0 Layer II, 24 kHz Mono @ 64 kbit/s
AACDecoder: using decoder 'FAAD2'
```


## Misc / Bots  
Location: `services/misc/`  
Restart: `docker compose restart`  


### BrigadersHelper
Purpose: Python Discord bot for server management and automation

Location: `services/BrigadersHelper`
Restart: `sudo systemctl restart BrigadersHelper`

Automation:
- Auto-runs as a systemctl service in `/etc/systemd/system/brigadershelper.service`
- Will send a message to discord whenever the Pi hangs (`cannot write to closing transport`) or is rebooted

```
[Unit]
Description=Baguette Brigaders Helper Discord Bot service
After=multi-user.target

[Service]
Type=simple
Restart=always
RestartSec=1
User=draggie
ExecStart=/home/draggie/services/BrigadersHelper/run.sh
WorkingDirectory=/home/draggie/services/BrigadersHelper

[Install]
WantedBy=multi-user.target
```

External access: https://brigaders-stats.ibaguette.com

### DraggieGamesServer
Purpose: Python webserver for Draggie Games accounts, auth, downloading, etc. Used to be my A Level NEA. 

Location: `services/DraggieGamesServer`
Restart: `sudo systemctl restart draggiegames`

Automation:
- Auto-runs as a systemctl service in `/etc/systemd/system/draggiegames.service`

```[Unit]
Description=client.draggie.games server service
After=multi-user.target

[Service]
Type=simple
Restart=always
RestartSec=1
User=draggie
ExecStart=/home/draggie/services/DraggieGamesServer/run_script.sh
WorkingDirectory=/home/draggie/services/DraggieGamesServer

[Install]
WantedBy=multi-user.target
```

External access: `client.draggie.games` (Cloudflare Tunnel)


### hacknotts-25
Purpose: Python webserver for running the HackNotts 25 project leaderboard

Location: `/mnt/ssd1/services/hacknotts-25`
Restart: `sudo systemctl restart hacknotts-25`

Automation:
- Auto-runs as a systemctl service in `/etc/systemd/system/hacknotts-25.service`

```[Unit]
Description=HackNotts 25 Leaderboard SEvice
After=multi-user.target

[Service]
Type=simple
Restart=always
RestartSec=1
User=draggie
ExecStart=/mnt/ssd1/services/hacknotts-25/run.sh
WorkingDirectory=/mnt/ssd1/services/hacknotts-25

[Install]
WantedBy=multi-user.target
```

External access: `hn25.ibaguette.com` (Cloudflare Tunnel)

### minecraft-whitelist
Purpose: Python Discord bot configured to run whitelist commands for a given server

Location: `/mnt/ssd1/services/minecraft-whitelist`
Restart: `sudo systemctl restart minecraft-whitelist`

Automation:
- Auto-runs as a systemctl service in `/etc/systemd/system/minecraft-whitelist.service`

```[Unit]
Description=Minecraft Whitelist Bot
After=multi-user.target

[Service]
Type=simple
Restart=always
RestartSec=1
User=draggie
ExecStart=/mnt/ssd1/services/minecraft-whitelist/run.sh
WorkingDirectory=/mnt/ssd1/services/minecraft-whitelist

[Install]
WantedBy=multi-user.target
```


## Remote Access

### pivpn
Runs on startup. Use Wireguard app to connect.

Run `pivpn -a` to setup a new QR code to scan in the Wireguard app.

# Automated tasks

## Cron jobs

\[Current user]

- Agile Octopus: Stop immich (transcoding) jobs before peak rates, and restart them after the 12p penalty is over
	- `49 15 * * * bash /home/draggie/services/immich-app/agile-cron.sh`
	- `0 19 * * * bash /home/draggie/services/immich-app/agile-cron-restart-jobs.sh`

- Auto-commit uni notes Obsidian changes and update the Git repo with new changes
	- `0 0 * * * cd /mnt/mega/uni-notes-git/ && /usr/bin/rclone sync --exclude .git/ --exclude .github/ r2:notes . -v && /usr/bin/git add . && /usr/bin/git commit -m "[cron] auto commit: update notes" && /usr/bin/git push &>> /mnt/mega/notes_sync.log`

- iPlayer Download task
	- `53 19 * * * bash /home/draggie/iplayer.sh > /mnt/mega/ipayer_log.txt`

