# Nginx Proxy Manager Homelab

A hands-on reverse proxy lab deployed with Docker Compose on a Windows 11 / WSL2 homelab host.

## Project Goals

- Deploy Nginx Proxy Manager with Docker Compose
- Persist application and certificate data outside the container
- Create and validate the administrative account
- Configure a first reverse proxy host
- Route a friendly local hostname to an existing Docker service
- Verify reverse proxy behavior end-to-end
- Validate restart behavior and configuration persistence
- Review logs and container resource usage
- Document troubleshooting encountered during the build
- Defer network-wide DNS and trusted internal TLS to the future pfSense/networking phase

## Skills Demonstrated

- Docker Compose service deployment
- Reverse proxy administration
- HTTP proxy routing
- Persistent container storage
- Port publishing
- Local hostname resolution
- Windows hosts-file troubleshooting
- Nginx Proxy Manager administration
- Container logging and inspection
- Restart policy validation
- Resource monitoring
- Troubleshooting authentication and DNS issues

## Lab Environment

| Component | Configuration |
|---|---|
| Host | GEEKOM Air12 Lite |
| OS | Windows 11 Pro |
| Docker backend | WSL2 |
| Docker host LAN IP | `192.168.0.181` |
| Nginx Proxy Manager | `jc21/nginx-proxy-manager:2.16.0` |
| Admin UI | Host port `81` |
| HTTP | Host port `80` |
| HTTPS | Host port `443` |
| Backend test service | Docker Nginx test service on host port `8081` |
| Test hostname | `docker-test.home.arpa` |

> `192.168.0.181` is an RFC1918 private LAN address used only inside the local network.

## Architecture

```text
Client Browser
      |
      | http://docker-test.home.arpa
      v
Local name resolution
      |
      | docker-test.home.arpa -> 192.168.0.181
      v
Nginx Proxy Manager :80
      |
      | forwards to http://192.168.0.181:8081
      v
Docker Nginx Test Service
      |
      v
Docker Homelab is Working
```

## Deployment

```yaml
services:
  app:
    image: jc21/nginx-proxy-manager:2.16.0
    container_name: nginx-proxy-manager
    restart: unless-stopped
    ports:
      - "80:80"
      - "81:81"
      - "443:443"
    volumes:
      - ./data:/data
      - ./letsencrypt:/etc/letsencrypt
```

Start and verify:

```powershell
docker compose up -d
docker compose ps
docker compose logs --tail 50
```

## First Proxy Host

```text
Domain: docker-test.home.arpa
Scheme: http
Forward Host/IP: 192.168.0.181
Forward Port: 8081
```

A temporary Windows hosts-file entry was used:

```text
192.168.0.181 docker-test.home.arpa
```

The final browser test successfully displayed:

```text
Docker Homelab is Working
```

## Persistence Validation

The container was recreated:

```powershell
docker compose down
docker compose up -d
```

After recreation, the administrator account and proxy host remained available.

## Resource Usage

Observed usage was roughly:

```text
CPU: near 0%
Memory: ~78-84 MB
```

## Deferred Work

The following are intentionally deferred to the pfSense/networking phase:

- network-wide internal DNS
- trusted internal HTTPS/TLS
- centralized DNS host overrides
- firewall/VLAN policy
- internal certificate strategy

## Repository Structure

```text
nginx-proxy-manager-homelab/
├── README.md
├── lessons-learned.md
├── .gitignore
├── compose/
│   └── compose.yaml
├── docs/
│   ├── 01-deployment.md
│   ├── 02-admin-setup.md
│   ├── 03-persistent-storage.md
│   ├── 04-first-proxy-host.md
│   ├── 05-local-name-resolution.md
│   ├── 06-troubleshooting.md
│   └── 07-final-validation.md
└── screenshots/
    └── README.md
```

## Status

**Project 2 - Nginx Proxy Manager: Complete**

Next planned homelab project: **Uptime Kuma**
