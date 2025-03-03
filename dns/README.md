# Pi-hole, Unbound, Keepalived & Lighttpd Setup

This repository provides a Docker Compose configuration that deploys a complete network filtering and DNS resolution solution using Pi-hole, Unbound, Keepalived, and Lighttpd. The stack is designed to block unwanted content, securely resolve DNS queries, and provide high availability via a virtual IP.

---

## Overview

- **Pi-hole**: Acts as a network-level ad blocker and tracker blocker.
- **Unbound**: Serves as a validating, recursive, and caching DNS resolver.
- **Keepalived**: Manages a Virtual IP (VIP) to ensure high availability.
- **Lighttpd**: Serves the Pi-hole web interface on a custom port.

---

## Services

### Pi-hole

- **Image**: `pihole/pihole:${PIHOLE_VERSION:-2024.07.0}`
- **Network Mode**: Host (ensures direct access to network interfaces)
- **Key Configurations**:
  - Uses environment variables to set the timezone, web password, and DNS forwarding (to Unbound at `127.0.0.1#5335`).
  - Runs its web interface on port `8010`.
  - Mounts persistent volumes for configuration and log data.
  - Granted additional network administration capabilities.

### Unbound

- **Image**: `mvance/unbound:${UNBOUND_VERSION:-1.22.0}`
- **Network Mode**: Host (listens on `127.0.0.1:5335`)
- **Key Configurations**:
  - Uses a custom configuration file (`unbound.conf`) that specifies logging, caching, DNSSEC, and access controls.
  - Mounts volumes to persist its configuration, root hints, and logs.
  - Tuned for performance with increased file descriptor limits.

### Keepalived

- **Image**: `osixia/keepalived:${KEEPALIVED_VERSION:-2.0.20}`
- **Network Mode**: Host (required for managing VIPs)
- **Key Configurations**:
  - Sets up a Virtual IP (`10.2.1.20/24`) on the `br0` interface.
  - Configured via the `keepalived.conf` file with VRRP settings, including authentication and priority for master status.
  - Requires elevated privileges for network administration.

---

## Configuration Files

### docker-compose.yaml

Defines the three main services (Pi-hole, Unbound, and Keepalived) with:
- **Environment Variables**: Customize settings such as time zone, passwords, and port numbers.
- **Volumes**: Map host directories for persistent storage of configuration files, logs, and data.
- **Restart Policies**: All services are set to restart automatically unless stopped.
- **Capabilities**: Additional capabilities (e.g., `NET_ADMIN`) are enabled where necessary.

### keepalived.conf

Defines the VRRP instance for Keepalived:
- **State**: Configured as `MASTER` with a high priority (`100`).
- **Interface & VIP**: Binds to interface `br0` with the VIP `10.2.1.20/24`.
- **Authentication**: Uses a simple password (`secret`) for VRRP authentication.
  
Example snippet:
~~~conf
vrrp_instance VI_1 {
    state MASTER
    interface br0 
    virtual_router_id 51
    priority 100
    advert_int 1
    authentication {
        auth_type PASS
        auth_pass secret
    }
    virtual_ipaddress {
        10.2.1.20/24
    }
}
~~~

### lighttpd.conf

Configures Lighttpd to serve the Pi-hole web interface:
- **Modules**: Loads modules for index files, directory listing, static file handling, and URL normalization.
- **Port**: Listens on port `8010`.
- **Performance & Security**: Implements strict parsing and normalization of URLs to enhance security and consistency.
  
Key settings include:
~~~conf
server.port = 8010
server.feature-flags += ("server.h2proto" => "enable")
server.http-parseopts = (
  "header-strict" => "enable",
  "host-strict" => "enable",
  "url-normalize-required" => "enable",
  "url-ctrls-reject" => "enable",
  "url-path-2f-decode" => "enable"
)
~~~

### unbound.conf

Custom configuration for Unbound:
- **Interface & Port**: Listens on `127.0.0.1:5335`.
- **Logging & Caching**: Configured for minimal logging and efficient caching.
- **Security**: DNSSEC is enforced and access is limited to specific subnets.
- **Performance**: Buffer sizes and prefetching are tuned for optimal DNS resolution.
  
Example settings:
~~~yaml
server:
    interface: 127.0.0.1
    port: 5335
    do-ip4: yes
    do-udp: yes
    logfile: "/opt/unbound/etc/unbound/unbound.log"
    access-control: 127.0.0.0/8 allow
    access-control: 10.2.1.0/24 allow
    root-hints: "/opt/unbound/etc/unbound/root.hints"
    prefetch: yes
~~~

---

## Deployment

### Prerequisites

- [Docker](https://docs.docker.com/get-docker/)
- [Docker Compose](https://docs.docker.com/compose/install/)

### Steps

1. **Clone the Repository**:
   ~~~bash
   git clone https://github.com/yourusername/your-repo.git
   cd your-repo
   ~~~
2. **Review & Customize**:
   - Adjust environment variables, volume paths, or other settings in the `docker-compose.yaml`.
   - Modify `keepalived.conf`, `lighttpd.conf`, and `unbound.conf` as needed for your network environment.
3. **Deploy the Stack**:
   ~~~bash
   docker-compose up -d
   ~~~
4. **Access the Pi-hole Web Interface**:
   - Open your browser and navigate to: [http://10.2.1.20:8010](http://10.2.1.20:8010)

---

## Maintenance & Troubleshooting

- **Logs**: Check individual container logs using:
   ~~~bash
   docker logs pihole
   docker logs unbound
   docker logs keepalived
   ~~~
- **Network Interface**: Ensure that the `br0` interface is correctly configured on your host.
- **Data Persistence**: Configuration files and logs are stored under `/mnt/cache/docker-compose-data/`. Regular backups of this directory are recommended.
- **Updates**: To update any image version, change the version tag in the environment variables of `docker-compose.yaml` and restart the services.

---

## License

This project is licensed under the [MIT License](LICENSE).

---

For any questions or issues, please open an issue in the repository or contact the maintainer.

Happy filtering and resolving!
