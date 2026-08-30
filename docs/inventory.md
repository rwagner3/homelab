# Inventory

The hardware and active workloads below were verified on 2026-08-30. Capacity
figures use the device manufacturers' decimal units.

## Hosts

| Host | Platform | Processor | Memory | Storage | Network |
| --- | --- | --- | ---: | --- | --- |
| Tower | Unraid 7.3.2; Gigabyte Z390 AORUS MASTER | Intel Core i7-8700K | 16 GB | One 24 TB parity disk; six 16 TB data disks; two 2 TB NVMe cache devices; LSI SAS3008 HBA | Realtek RTL8125 2.5GbE |
| Morefine M9S | Home Assistant OS | Intel N305 | 16 GB | 512 GB NVMe | 1GbE |
| GMKtec M3 Ultra | Ubuntu 24.04 | Intel Core i7-12700H | 32 GB | 1 TB NVMe | 2.5GbE |
| Clawbox, Acer Nitro AN515-45 | Pop!_OS 24.04 | AMD Ryzen 7 5800H | 16 GB | 512 GB NVMe | Wi-Fi; NVIDIA RTX 3060 Laptop GPU with 6 GB VRAM |
| Cognea | Windows 11 Pro with WSL2; Gigabyte Z690 UD AX DDR4 | Intel Core i9-13900K | 128 GB | 4 TB NVMe | 2.5GbE adapter, observed at a 1 Gbps link; NVIDIA RTX 5090 with 32 GB VRAM |

## Workloads by host

| Host | Active workloads |
| --- | --- |
| Morefine M9S | Home Assistant, Frigate, MQTT |
| GMKtec M3 Ultra | SearXNG, Tdarr worker, Beszel agent |
| Clawbox | OpenClaw, SearXNG, Tdarr worker, Music Radar |
| Cognea | SearXNG, Tailscale |

### Tower applications

Tower's application inventory lists user-facing or operational services first.
Supporting containers remain grouped with the application that owns them.

| Role | Primary applications | Associated components |
| --- | --- | --- |
| Navigation and access | Homepage | Tailscale integration |
| Media library | Plex, Tautulli, Pinchflat | None |
| Media acquisition | Prowlarr, Sonarr, Radarr, SABnzbd, qBittorrent | Gluetun for qBittorrent; Tailscale integrations for Prowlarr, Sonarr, and Radarr |
| Distributed transcoding | Tdarr server | Workers run on GMKtec and Clawbox |
| Photo management | Immich | Machine learning, Postgres, Valkey, Tailscale sidecar |
| Personal applications | Mealie, Hammond, Music Radar | Music Radar dashboard and scheduler; Tailscale sidecars for Hammond and Music Radar |
| Source control | Gitea | Tailscale integration |
| Monitoring | Uptime Kuma, Beszel, Scrutiny, Speedtest Tracker | Beszel agent |

Stopped containers and offline Tailscale entries are not current workloads.
Household endpoints, other desktop systems, Raspberry Pis, and personal devices
are outside this inventory.
