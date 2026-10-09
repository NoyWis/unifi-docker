# UniFi Network Application in Docker

Self-hosted UniFi controller (linuxserver.io image) with a dedicated MongoDB 7 container.
I use it to manage UniFi access points and switches without a Cloud Key.

## What's inside
- MongoDB 7 with a healthcheck. The controller starts only after the database is ready
- Credentials come from `.env`, never from the compose file
- Persistent volumes for the database (`./db`) and the controller config (`./config`)
- Ports documented: inform, STUN, discovery, guest portal
- `:Z` volume labels, so it works on SELinux hosts (Fedora/RHEL) with Docker or Podman

## Quick start
```bash
cp .env.example .env      # set MONGO_PASS
docker compose up -d
```
Open `https://<host>:8443` and follow the setup wizard.

To adopt devices, set the inform URL on the AP:
```bash
ssh ubnt@<ap-ip>
set-inform http://<controller-ip>:8080/inform
```

## Stack
Docker Compose · MongoDB 7 · UniFi Network Application
