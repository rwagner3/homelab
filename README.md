# homelab

## Containers

- [tailscale](https://tailscale.com/): 
This lets me connect to my servers and containers, securely from anywhere in the world. I highly recommend this VPN because of how simple it is to get setup, and is free for up to 100 devices and 3 users.

- [homepagedev](https://gethomepage.dev/):
Gives you a... homepage, for all your containers and services. All yaml driven and very simple. It lets configure siteMonitors and widgets to test connectivity and see what the container/service is doing, at a glance.

- Immich: Google Photos replacement

- Arr Stack:
  - Prowlarr: Indexer manager for Usenet and Torrents
  - Sonarr: Find TV Shows
  - Radarr: Find Movies
  - SABnzbd: Usenet download client
  - qBittorrent: Torrent download client
    - GluetunVPN: For torrents only, I use a paid for VPN service thru this container
  - Plex: I bought a lifetime pass a long time back, which has kept me locked in with Plex. I've heard good things about other Media players, but this works for me
  - Pinchflat: Youtube channel scraper

- Odds and Ends
  - LibreChat: Centralized AI chat. Lets you use your API keys from all the major players in a single chat interface.
  - Hammond: Vehicle Expense tracking
  - Mealie: Recipe management, includes AI webscraper to injest recipes into a local DB
  - Beaver Habit Tracker: A basic habit tracker, so you can make sure you are exercizing or whatever
 
- Monitoring:
  - UptimeKuma: Uptime monitoring and alerting for service endpoints
  - Beszel: Lightweight, simple, centralized container monitoring
  - Beszel-agent: Agent that connects to the beszel server, needs to be installed on each server you run containers on
  - Scrutiny: Disk health and SMART monitoring
  - Speedtest Tracker: Internet speed tracking and monitoring
  - Tautulli: Analytics for Plex
 
- DNS:
  - Unbound: Non-forwarding recursive DNS resolver
  - Pihole: Network level Adblocking
  - Keepalived: virtual IP to allow for HA Pihole

## Layer 1 Network

- ISP: GloFiber 1.2 Gbps bidirectional
- Router: [Cloud Gateway Max](https://store.ui.com/us/en/category/cloud-gateways-compact/collections/cloud-gateway-max/products/ucg-max-ns?variant=ucg-max-ns)
- PoE Switchs:
  - [8 port Flex 2.5G PoE](https://store.ui.com/us/en/category/all-switching/products/usw-flex-2-5g-8-poe) - located in the living room closet
  - [8 port Lite PoE](https://store.ui.com/us/en/category/all-switching/products/usw-lite-8-poe) - located in the upstairs office
- APs:
  - [U7 Pro Max](https://store.ui.com/us/en/category/all-wifi/products/u7-pro-max) - 2nd floor Office AP
  - [U7 Pro](https://store.ui.com/us/en/category/wifi-flagship/products/u7-pro) - 1st floor Living Room AP

 ```mermaid
graph TD
  A["Internet<br>1.2 Gbit<br>Living Room"] -->|WAN| B["Router<br>Cloud Max 4-port 2.5 Gbit<br>Living Room"]
  B --> D["Switch<br>PoE 8-port 2.5 Gbit<br>Living Room"]
  B --> E["Switch<br>PoE 8-port 1 Gbit<br>Office"]
  B --> F["2x Empty"]
  D --> G["AP<br>U7 Pro Max<br>Upstairs"]
  D --> H["Laptop<br>Mom 1 Gbit<br>Living Room"]
  D --> C["Server<br>UnRAID 1 Gbit<br>Living Room"]
  D --> I["AP<br>U7 Pro<br>Living Room"]
  D --> J["4x Empty"]
%%  D --> K[Empty]
%%  D --> L[Empty]
%%  D --> M[Empty]
  E --> N["4x Empty"]
%%  E --> O[Empty]
  E --> P["Server<br>Morefine HA 1 Gbit<br>Office"]
  E --> Q["PC<br>Son 1 Gbit<br>Office"]
  E --> R["Arlo (gone soon)"]
%%  E --> S[Empty]
%%  E --> T[Empty]
```

## Hardware

- [unRAID](https://unraid.net/): Just an assortment of hardware to handle most of my compute and all my storage. I love unRAID so much, because it handles nearly everything I hate about long term server ownership, OS and application management, and simplifies it.
  - CPU: i7-8700K Intel
  - MB: Z370-Plus Asus
  - Mem: 32 GB Mem
  - HBA: LSI SAS2008 PCI-Express Fusion-MPT SAS-2, 8 ports
  - HDD: 5x 16TB Seagate Exos X18
  - NVMe:
    - appdata on 1TB Samsung EVO Plus
    - download cache and Immich files on 2TB Samsung EVO Plus
 
- Couple Raspberry Pi 3B's
