# 🛑 Immich on Proxmox LXC with Docker

Quick guide to install **Immich** (self-hosted photo/video management) inside a Proxmox **LXC** container using Docker Compose.

---

## 1 — Install Docker (Alpine example)

```bash
apk add docker docker-compose
service docker start
docker ps   # verify it's running
```

Auto-start on boot:
```bash
rc-update add docker boot
```

---

## 2 — Project folder

```bash
mkdir immich-app && cd immich-app
```

---

## 3 — `docker-compose.yml`

Get the latest official file directly:
```bash
wget -O docker-compose.yml https://github.com/immich-app/immich/releases/latest/download/docker-compose.yml
```

> 🔧 To disable machine learning (face/object recognition) and save RAM/CPU, just delete the `immich-machine-learning:` service block.

---

## 4 — `.env` file

```bash
wget -O .env https://github.com/immich-app/immich/releases/latest/download/example.env
```

Then edit it:
```env
UPLOAD_LOCATION=./library
DB_DATA_LOCATION=./postgres
TZ=Europe/Rome
IMMICH_VERSION=release
DB_PASSWORD=your_secure_password   # letters/numbers only
DB_USERNAME=postgres
DB_DATABASE_NAME=immich
```

---

## 5 — Fix timezone (Alpine only, if needed)

```bash
apk add tzdata
cp /usr/share/zoneinfo/Europe/Rome /etc/localtime
echo "Europe/Rome" > /etc/timezone
```

---

## 6 — Start Immich

```bash
docker compose up -d
```
---
## 9 — Access Immich

```
http://<LXC_IP>:81
```
---
