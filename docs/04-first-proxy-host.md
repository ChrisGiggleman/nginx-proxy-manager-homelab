# 04 - First Proxy Host

Backend:

```text
http://192.168.0.181:8081
```

Proxy host:

```text
Domain: docker-test.home.arpa
Scheme: http
Forward Host/IP: 192.168.0.181
Forward Port: 8081
```

Successful result:

```text
http://docker-test.home.arpa
```

returned:

```text
Docker Homelab is Working
```
