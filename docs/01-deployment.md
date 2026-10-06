# 01 - Deployment

Project directory:

```powershell
mkdir C:\Docker-Lab\nginx-proxy-manager
cd C:\Docker-Lab\nginx-proxy-manager
```

The Compose deployment publishes ports 80, 81, and 443 and uses persistent `data` and `letsencrypt` directories.

Initial issue:

```text
empty compose file
```

Cause: `compose.yaml` existed but had not been saved with content.

Resolution:

```powershell
docker compose config
docker compose up -d
docker compose ps
docker compose logs --tail 50
```

Admin UI:

```text
http://192.168.0.181:81
```
