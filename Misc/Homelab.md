
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
- /etc/docker/daemon.json

```json
{
	"min-api-version": "1.41",
	"data-root": "/mnt/ssd1/docker"
}
```
- https://github.com/portainer/portainer/issues/12925#issuecomment-3560758801



## Misc Tools

- Get hard drive temperatures:
	- `sudo smartctl -a /dev/sdb | grep "194"`
	- `sudo smartctl -a /dev/sdb` *(all SMART data)*

## System

- Reboot
	- `sudo reboot`
- Update all packages system-wide:
	- `sudo apt-get update && sudo apt-get upgrade --autoremove -y`
- Current usage/task manager
	- `htop`
	- Normal mem usage: 4-5G/7.87G (Swap usage often gets to 2gb, do not worry.)

- Fstab entries `sudo nano /etc/fstab`
	- SSD Cache (usb3->sata) (256gb) `UUID=d6ecfcd5-2703-41bf-9301-10c403b6fb0c /mnt/ssd1 ext4 nofail,defaults 0 2`
	- External 20tb drive (usb3) `UUID=302749e2-3434-4b3f-b3b8-d36a7df58ac0 /mnt/mega ext4 nofail,defaults 0 2`
- Swapfile/ram config `sudo nano /etc/dphsys-swapfile`
	- `CONF_SWAPFILE=/mnt/ssd1/swap`
	- `CONF_SWAPSIZE=2048`
# Services Breakdown

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


docker-compose.yml: 
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

## Network & Monitoring Stack  
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
Purpose: Apple ID server for sign-in/token services.  

### Pi-hole
Access: http://192.168.1.3/admin
Purpose: Assign DHCP addresses to all devices on the network and act as an authoritative DNS server for each


---

## Misc / Bots  
Location: `services/misc/`  
Restart: `docker compose restart`  

### MinMaxOctopusBot  
Access: Internal only.
Purpose: Octopus energy automatic tariff switcher.
Logs: `docker logs MinMaxOctopusBot | tail`

Automation:
- Runs every night at 23:00

Documentation:
- https://github.com/eelmafia/octopus-minmax


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

## Remote Access

### pivpn

Runs on startup. Use Wireguard app to connect.

Run `pivpn -a` to setup a new QR code to scan in the Wireguard app.


# Automations

## Cron jobs

\[Current user]

- Agile Octopus: Stop immich (transcoding) jobs before peak rates, and restart them after the 12p penalty is over
	- `49 15 * * * bash /home/draggie/services/immich-app/agile-cron.sh`
	- `0 19 * * * bash /home/draggie/services/immich-app/agile-cron-restart-jobs.sh`

- Auto-commit uni notes Obsidian changes and update the Git repo with new changes
	- `0 0 * * * cd /mnt/mega/uni-notes-git/ && /usr/bin/rclone sync --exclude .git/ r2:notes . -v && /usr/bin/git add . && /usr/bin/git commit -m "[cron] auto commit: update note>0 0 * * * cd /mnt/mega/uni-notes-git/ && /usr/bin/rclone sync --exclude .git/ --exclude .github/ r2:notes . -v && /usr/bin/git add . && /usr/bin/git commit -m "[cron] auto commit: update notes" && /usr/bin/git push &>> /mnt/mega/notes_sync.log`

- iPlayer Download task
	- `53 19 * * * bash /home/draggie/iplayer.sh > /mnt/mega/ipayer_log.txt`

