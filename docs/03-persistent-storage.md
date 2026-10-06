# 03 - Persistent Storage

Bind mounts:

```yaml
volumes:
  - ./data:/data
  - ./letsencrypt:/etc/letsencrypt
```

Restart policy:

```powershell
docker inspect nginx-proxy-manager --format '{{.HostConfig.RestartPolicy.Name}}'
```

Result:

```text
unless-stopped
```

Persistence was verified by recreating the stack:

```powershell
docker compose down
docker compose up -d
```

After recreation, the admin account and proxy host were still present.
