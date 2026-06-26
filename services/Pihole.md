# 🛑 Pi-hole Setup Notes

**Pi-hole** is a network-wide ad blocker that acts as a DNS sinkhole,blocking advertisements and tracking domains for all devices on the network. It is lightweight and resource-efficient, requiring very little memory to run.

---

##  How to Install Pi-hole

For this installation, I used a **Linux Container (LXC)** running **Ubuntu Server** inside Proxmox.

### 📋 Prerequisites
Before running the installer, make sure your system package list is up to date and that `curl` is installed. Run the following commands:
```bash
sudo apt update && sudo apt install curl -y
curl -sSL https://install.pi-hole.net | bash
```
##  Post-Installation Configuration

Now that Pi-hole is successfully installed via the CLI, you need to configure your devices to use it. 

To start blocking ads, go to your device's **Network Settings** and change the primary **DNS server address** to the local **IP address of your Pi-hole LXC container**.

>  **Important Note:** Make sure that your Pi-hole container has a **static IP address** assigned within Proxmox.

##  Dashboard Overview
Below is the visual overview of my **Pi-hole Dashboard**:

![Pihole_dashboard](../images/pihole.png)
