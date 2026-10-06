# 05 - Local Name Resolution

Initial error:

```text
DNS_PROBE_FINISHED_NXDOMAIN
```

Cause: no DNS record existed for the local hostname.

Temporary validation method:

```text
192.168.0.181 docker-test.home.arpa
```

added to the Windows hosts file.

DNS cache refresh:

```powershell
ipconfig /flushdns
```

This worked on the test Windows client only.

Network-wide internal DNS is intentionally deferred to the pfSense/networking project.
