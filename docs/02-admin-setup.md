# 02 - Administrative Setup

The first admin-account attempt resulted in an invalid email/password login.

Logs showed the setup workflow running and the persistent directory contained `database.sqlite`, confirming that application state was being written.

Because the deployment was brand new, the application state was reset safely:

```powershell
docker compose down
Remove-Item -Recurse -Force .\data
Remove-Item -Recurse -Force .\letsencrypt
docker compose up -d
```

The administrator account was then recreated successfully.
