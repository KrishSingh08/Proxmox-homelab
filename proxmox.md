# 🟠Proxmox VE: Quick Installation Guide

---

## 💡 1. Before Installation
* **Enable Virtualization:**
---

## 💡 2. Installation
1. **Download the ISO:** Get Proxmox VE from the official website.
2. **flash the iso into the USB:** Using **Rufus**
3. **Boot & Setup:** Boot your computer from the USB, select *Install Proxmox VE (Graphical)*, and follow the steps:
   * Accept the EULA and select the target installation drive.
   * Set your Country, Time Zone, and Keyboard Layout.
   * Create a password for the **root** user and enter your email.
   * Configure the network by entering your **Static IP**, **Subnet Mask**, **Gateway**, and **DNS**.
4. **Reboot:**

---

## 💡 3. First Access
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

##  Verification
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
## 💡 5. SSH Key Configuration
Follow these steps to generate an SSH key on Windows and configure your remote server to use key-based authentication.
---
### Phase 1: Generate SSH Key on Windows
Open your **Windows Terminal** and generate a new 4096-bit RSA key pair:
```bash
ssh-keygen -t rsa -b 4096
```

Once generated, display your **public key** so you can copy it:

```bash
cat ~/.ssh/id_rsa.pub
```

Copy the entire output — you'll need it in the next phase.
---

### Phase 2: Configure the Remote Server (Linux)
Create the `.ssh` directory if it doesn't already exist, and set the correct permissions:

```bash
mkdir -p ~/.ssh
chmod 700 ~/.ssh
```
Open (or create) the `authorized_keys` file:
```bash
nano ~/.ssh/authorized_keys
```
Paste your **public key** 
Set the correct permissions on the file:
```bash
chmod 600 ~/.ssh/authorized_keys
```
---

### Phase 3: configure the sshd_config

Edit the SSH daemon configuration file:

```bash
sudo nano /etc/ssh/sshd_config
```
Make sure the following options are set:

```ini
PermitRootLogin no
PubkeyAuthentication yes
```

Save and exit, then restart the SSH service to apply the changes:

```bash
sudo systemctl restart ssh
```

---


