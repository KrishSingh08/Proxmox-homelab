# 🛑 Vaultwarden Setup Notes
##  How to Install Vaultwaraden
for this installation,I used  a **Linux Container (LXC)** running **Alpine ** inside Proxmox.
 Run the following commands:
```bash 
apk add docker docker-compose #To install docker 
rc-service docker start   # Is the systemctl of alpine, used to start docker
rc-update add docker boot   # this command start docker when booting the lxc
```
---
##  Create the docker-compose.yml file 
```bash
services:
  vaultwarden:
    container_name: vaultwarden
    image: vaultwarden/server:latest
    restart: unless-stopped
    volumes:
      - ./data/:/data/
    ports:
      - XXXX:80
    environment:
      - DOMAIN=https://subdomain.yourdomain.com
      - LOGIN_RATELIMIT_MAX_BURST=10
      - LOGIN_RATELIMIT_SECONDS=60
      - ADMIN_RATELIMIT_MAX_BURST=10
      - ADMIN_RATELIMIT_SECONDS=60
      - ADMIN_TOKEN=YourReallyStrongAdminTokenHere
      - SENDS_ALLOWED=true
      - EMERGENCY_ACCESS_ALLOWED=true
      - WEB_VAULT_ENABLED=true
      - SIGNUPS_ALLOWED=false
      - SIGNUPS_VERIFY=true
      - SIGNUPS_VERIFY_RESEND_TIME=3600
      - SIGNUPS_VERIFY_RESEND_LIMIT=5
      - SIGNUPS_DOMAINS_WHITELIST=yourdomainhere.com,anotherdomain.com
      - SMTP_HOST=smtp.youremaildomain.com
      - SMTP_FROM=vaultwarden@youremaildomain.com
      - SMTP_FROM_NAME=Vaultwarden
      - SMTP_SECURITY=SECURITYMETHOD
      - SMTP_PORT=XXXX
      - SMTP_USERNAME=vaultwarden@youremaildomain.com
      - SMTP_PASSWORD=YourReallyStrongPasswordHere
      - SMTP_AUTH_MECHANISM="Mechanism"
```
>  **source:** https://www.techaddressed.com/tutorials/vaultwarden-docker-compose/
---
##  start the docker compose file using:
```bash
docker compose up -d
```
---
## Access vaultwarden
```
http://<domain from nginx >:8000
or
http://<LXC_ip >:8000
```
---
#  Chrome → Vaultwarden

**Export:** Chrome → `chrome://password-manager/settings` → ⋮ next to "Saved Passwords" → **Export passwords** → confirm identity → save the `.csv`

**Import:** Log into your Vaultwarden vault → **Tools → Import Data** → format **Chrome (csv)** → choose your file → **Import Data**

**Then:** delete the `.csv` file immediately — it's plain text, anyone can read it. Don't import the same file twice (no duplicate check).
