# 06 - Troubleshooting

## Empty Compose File

Symptom:

```text
empty compose file
```

Resolution: save the YAML, validate with `docker compose config`, then redeploy.

## Admin Login Failure

The first-run admin account did not authenticate correctly.

Because the deployment contained no production configuration, the persistent application state was reset and the admin account was recreated.

## PowerShell Path Entered as a Command

Typing a folder path directly produced a command-not-found error.

Use:

```powershell
cd C:\Docker-Lab\nginx-proxy-manager
```

## NXDOMAIN

The local hostname failed because no DNS record existed.

A temporary Windows hosts-file entry was used.

## Hosts File Permission Issue

The hosts file could not be saved from the editor.

An elevated PowerShell session was used:

```powershell
Add-Content -Path "C:\Windows\System32\drivers\etc\hosts" -Value "`r`n192.168.0.181 docker-test.home.arpa"
```
