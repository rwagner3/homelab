# homelab

This repository documents a small self-hosted network built around an Unraid
storage server, dedicated Home Assistant hardware, two Linux compute nodes, and
a Windows workstation with WSL2. A UniFi Cloud Gateway Max routes six VLANs and
connects two switches and two wireless access points.

The current inventory was verified on 2026-08-30. See the detailed
[network map](docs/network.md) and [host inventory](docs/inventory.md).

## At a glance

- GloFiber 1.2 Gbps symmetric internet through a UCG-Max
- Tower provides storage, media, photo management, personal applications, and
  monitoring
- A Morefine M9S runs Home Assistant OS, Frigate, and MQTT
- GMKtec and Clawbox provide search, automation, and distributed media work
- Cognea provides a Windows 11 and WSL2 compute environment
- Tailscale connects selected hosts and services without exposing them directly
  to the public internet

The retired Pi-hole, Unbound, and Keepalived configuration remains under
[`dns/`](dns/README.md) as a historical reference. It is not part of the current
DNS path.

## Verification scope

"Current" means observed active on 2026-08-30 through read-only UniFi API
requests, SSH inventory commands, Docker status, Tailscale status, or the Home
Assistant OS observer. The public documentation omits credentials, MAC
addresses, public WAN details, personal endpoints, switch-port numbers, SSIDs,
and Tailscale addresses and domains.
