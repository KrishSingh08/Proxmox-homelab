# Proxmox VE: Quick Installation Guide

---

## 1. Before Installation
* **Enable Virtualization:**
---

## 2. Installation
1. **Download the ISO:** Get Proxmox VE from the official website.
2. **flash the iso into the USB:** Using **Rufus**
3. **Boot & Setup:** Boot your computer from the USB, select *Install Proxmox VE (Graphical)*, and follow the steps:
   * Accept the EULA and select the target installation drive.
   * Set your Country, Time Zone, and Keyboard Layout.
   * Create a password for the **root** user and enter your email.
   * Configure the network by entering your **Static IP**, **Subnet Mask**, **Gateway**, and **DNS**.
4. **Reboot:**

---

## 3. First Access
1. **Access the Web GUI:** 
   `https://<YOUR_STATIC_IP>:8006/`
2. **Login:** 
   * **Username:** `root`
   * **Password:**
U have finally installed Proxmox on your device
---

## 💡 4. Post-Install Automation Script (Optional)
To instantly remove the subscription warning , open the Proxmox **Shell** and run this command:
```bash
bash -c "$(wget -qLO - [https://github.com/community-scripts/ProxmoxVE/raw/main/scripts/pve-post-install.sh](https://github.com/community-scripts/ProxmoxVE/raw/main/scripts/pve-post-install.sh))"
```
## 4. Securing Proxmox: New User, Sudo, and Disabling Root

For security, it is highly recommended to create a standard user with `sudo` privileges and disable the default `root` login.

---

### Step 1: Create a New User via CLI
Open the Proxmox Shell and run:
```bash
# Add the new user and set a password
adduser <username>

# Install sudo and add the user to the sudo group
apt update && apt install sudo -y
adduser <username> sudo
```

### 2. Add the User to the Cluster
1. On the left-side menu, click on **Datacenter**.
2. Select **Users** from the sub-menu.
3. Click the **Add** button at the top.
4. Click **Add** to save.

### 3. Assign Administrator Permissions
1. While still under **Datacenter**, click on **Permissions**.
2. Click the **Add** dropdown button and select **User Permission**.
3. Click **Add**.
---

## 💡 Verification
then u return to your terminal:
1. **Switch to your new user** to test their access:
   ```bash
   su - <username>
    ```
2. **disable root**:
 ```bash
sudo passwd -l root
 ```
---
