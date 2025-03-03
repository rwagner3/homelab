# HA Pihole with Unbound as Nonforwarding Recursive DNS Resolver

## Update root.hints file in Unbound

Once every ~6 months, you should update this file and restart Unbound, something like:
- `wget https://www.internic.net/domain/named.root -qO- | sudo tee root.hints`
