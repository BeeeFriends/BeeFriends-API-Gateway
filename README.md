# BeeFriends API Gateway

Reverse proxy gateway for one public BeeFriends backend domain.

---

## Purpose

The gateway keeps the mobile app pointed at one API base URL while routing requests to the correct backend service.

```txt
BeeFriends Mobile
  -> BeeFriends API Gateway
    -> User Service
    -> Match Chat Service
    -> Notification Service
```

---

## Stack

| Layer | Stack |
| ----- | ----- |
| Gateway | Caddy |
| Deploy | Railway |
| Config | `Caddyfile` |

---

## Routes

```txt
https://beefriends-be.drian.my.id/v1/user/*
-> https://user-services-beefriends-be-production.up.railway.app/v1/user/*

https://beefriends-be.drian.my.id/v1/matchchat/*
-> https://matchchat-service-beefriends-be-production.up.railway.app/v1/matchchat/*

https://beefriends-be.drian.my.id/v1/notifications*
-> https://notification-service-beefriends-be-production.up.railway.app/v1/notifications*

https://beefriends-be.drian.my.id/socket.io/*
-> https://matchchat-service-beefriends-be-production.up.railway.app/socket.io/*

https://beefriends-be.drian.my.id/health
-> ok
```

---

## Environment Variables

Railway injects `PORT`. Optional override:

```env
NOTIFICATION_SERVICE_URL=https://notification-service-beefriends-be-production.up.railway.app
```

---

## Deploy

1. Publish repo ini ke GitHub.
2. Deploy ke Railway sebagai service baru.
3. Pasang custom domain `beefriends-be.drian.my.id` ke service gateway ini.
4. Jangan pasang domain yang sama ke User Service, Match Chat Service, atau Notification Service.

Railway akan inject env `PORT`, dan Caddy listen ke `:{$PORT}`.

---

## Local Run

```bash
docker build -t beefriends-api-gateway .
docker run --rm -p 8080:8080 -e PORT=8080 beefriends-api-gateway
```
