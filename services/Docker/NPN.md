# 🛑 Nginx Proxy Manager Setup Notes

##  How to Install PNP
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
  app:
    image: 'jc21/nginx-proxy-manager:latest'
    restart: unless-stopped
    ports:
      - '80:80'
      - '81:81'
      - '443:443'
    volumes:
      - ./data:/data
      - ./letsencrypt:/etc/letsencrypt
```
---
##  start the docker compose file using:
```bash
docker compose up -d
```
---
## Access NPN
```
http://<LXC_IP>:2283
```
---
## Add a Certificate

To enable HTTPS, you'll first need a domain name. **DuckDNS** lets you create one for free.

 **Create a free domain**
   Go to [DuckDNS](https://www.duckdns.org) and register a subdomain (e.g. `yourname.duckdns.org`) pointing to your public IP.

 **Open the Certificates page**
   In your browser, go to:
   ```
   http://<LXC_IP>:81/certificates
   ```

 **Add a new certificate**
   - Click **Add Certificate**
   - Choose **Let's Encrypt via dns**
   - Choose **DuckDNS** as the DNS provider
   - Fill in the form with your DuckDNS domain and API token
   - into **Propagation Seconds** add 120 seconds.
   - Click **Save** and wait for the certificate to be issued
     

 **Add your hosts**
    go back to the main **Dashboard** and click **Add Proxy Host** to create a new host entry, assigning it the certificate you just generated.

---

