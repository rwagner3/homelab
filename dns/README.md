# Retired DNS stack

> **Retired:** This Pi-hole, Unbound, Keepalived, and Lighttpd configuration is
> historical and is not deployment-ready.

The UCG-Max at `10.2.1.1` provided DNS when the network was checked on
2026-08-30. The former Keepalived virtual address at `10.2.1.20` was inactive.
Nothing under this directory describes the current DNS path.

The files remain as an archive of the former design:

- Pi-hole accepted LAN DNS traffic and forwarded recursive lookups to Unbound
  on `127.0.0.1:5335`.
- Unbound performed recursive resolution and DNSSEC validation.
- Keepalived assigned `10.2.1.20/24` as a virtual address on `br0`.
- Lighttpd exposed the Pi-hole interface on port `8010`.

The Compose file and Keepalived configuration now contain explicit non-secret
placeholders. They still include old image versions, host paths, interface
names, privileges, and assumptions that have not been tested for reuse. Do not
deploy them without a full review.

Earlier commits contain the credential strings removed from the working tree.
Git history has not been rewritten. Treat those strings as compromised and
never reuse them.
