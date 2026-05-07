# BeeFriends API Gateway

Gateway reverse proxy untuk satu domain BeeFriends backend.

## Routes

```txt
https://beefriends-be.drian.my.id/v1/user/*
-> https://user-services-beefriends-be-production.up.railway.app/v1/user/*

https://beefriends-be.drian.my.id/v1/matchchat/*
-> https://matchchat-service-beefriends-be-production.up.railway.app/v1/matchchat/*

https://beefriends-be.drian.my.id/socket.io/*
-> https://matchchat-service-beefriends-be-production.up.railway.app/socket.io/*
```

## Deploy

1. Publish repo ini ke GitHub.
2. Deploy ke Railway sebagai service baru.
3. Pasang custom domain `beefriends-be.drian.my.id` ke service gateway ini.
4. Jangan pasang domain yang sama ke User Service atau MatchChat Service.

Railway akan inject env `PORT`, dan Caddy listen ke `:{$PORT}`.
