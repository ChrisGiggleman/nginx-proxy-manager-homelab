# Lessons Learned

- Validate Compose files before deployment with `docker compose config`.
- Persistent bind mounts make container recreation safe.
- Resetting state is reasonable early in a lab when no production configuration exists.
- Reverse proxy routing and DNS resolution are separate layers.
- A Windows hosts-file entry is useful for proof-of-concept testing but not scalable.
- Internal DNS belongs in the future networking/pfSense layer.
- Trusted internal TLS should be designed after DNS and firewall architecture are in place.
- Nginx Proxy Manager is lightweight enough for the current GEEKOM host.
