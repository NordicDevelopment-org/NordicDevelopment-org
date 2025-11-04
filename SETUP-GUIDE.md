# Comprehensive Setup Guide for Mesh Networking
## Reticulum, NomadNet, and MeshChat

This guide will walk you through setting up a complete mesh networking system using Reticulum, NomadNet, and MeshChat on Windows, macOS, Linux, and Raspberry Pi.

---

## Table of Contents

1. [Hardware Requirements](#hardware-requirements)
2. [Software Requirements](#software-requirements)
3. [Windows Setup](#windows-setup)
4. [macOS Setup](#macos-setup)
5. [Linux Setup](#linux-setup)
6. [Raspberry Pi Setup](#raspberry-pi-setup)
7. [Security Best Practices](#security-best-practices)
8. [Troubleshooting](#troubleshooting)

---

## Hardware Requirements

### Minimum Requirements
- **Computer/Device**: Any modern computer or Raspberry Pi 3B+ or newer
- **RAM**: 1GB minimum (2GB+ recommended)
- **Storage**: 2GB free space
- **Network**: Internet connection for initial setup

### Recommended Hardware for Mesh Networking
- **Radio Hardware** (for actual mesh networking):
  - RNode (recommended) - DIY or pre-built
  - LoRa modules (SX1276, SX1278, SX1262, SX1268)
  - WiFi adapters for local mesh
  - Serial modems
- **Raspberry Pi Users**:
  - Raspberry Pi 3B+, 4, or 5
  - MicroSD card (16GB+ recommended, Class 10)
  - Power supply (official recommended)
  - USB radio module or LoRa HAT

### Optional Hardware
- GPS module (for location services)
- External antenna (for better range)
- Portable battery pack (for mobile operation)

---

## Software Requirements

### Core Components
- **Python**: 3.7 or newer (3.9+ recommended)
- **pip**: Python package installer
- **Reticulum**: The networking stack
- **NomadNet**: Node and client application
- **MeshChat**: Chat application for mesh networks

### Operating System Support
- **Windows**: 10 or 11
- **macOS**: 10.15 (Catalina) or newer
- **Linux**: Any modern distribution (Ubuntu, Debian, Fedora, Arch, etc.)
- **Raspberry Pi OS**: Bullseye or newer (64-bit recommended)

---

## Windows Setup

### Step 1: Install Python

1. **Download Python**:
   - Visit [python.org/downloads](https://www.python.org/downloads/)
   - Download Python 3.11 or newer for Windows
   - **Important**: Check "Add Python to PATH" during installation

2. **Verify Installation**:
   Open PowerShell or Command Prompt and run:
   ```powershell
   python --version
   ```
   ```powershell
   pip --version
   ```

### Step 2: Install Visual C++ Build Tools (Required)

Some Python packages need compilation tools:

1. Download Visual Studio Build Tools from [visualstudio.microsoft.com](https://visualstudio.microsoft.com/downloads/)
2. Install "Desktop development with C++" workload

   **OR** use the simplified installer:
   ```powershell
   winget install Microsoft.VisualStudio.2022.BuildTools
   ```

### Step 3: Install Reticulum

Open PowerShell or Command Prompt as Administrator:

```powershell
pip install rns
```

Verify installation:
```powershell
rnsd --version
```

### Step 4: Install NomadNet

```powershell
pip install nomadnet
```

Verify installation:
```powershell
nomadnet --version
```

### Step 5: Install MeshChat

```powershell
pip install meshchat
```

Verify installation:
```powershell
meshchat --version
```

### Step 6: Initialize Configuration

Create configuration directories and files:

```powershell
# Initialize Reticulum
rnsd --version
```

This creates the configuration at: `%USERPROFILE%\.reticulum\`

```powershell
# Initialize NomadNet
nomadnet --daemon
```

Configuration location: `%USERPROFILE%\.nomadnet\`

### Step 7: Start Services

**Start Reticulum (in one PowerShell window):**
```powershell
rnsd
```

**Start NomadNet (in another PowerShell window):**
```powershell
nomadnet
```

**Start MeshChat (in another PowerShell window):**
```powershell
meshchat
```

### Optional: Create Desktop Shortcuts

Save this as a `.bat` file to quick-launch:

**start-reticulum.bat:**
```batch
@echo off
start "Reticulum" cmd /k rnsd
start "NomadNet" cmd /k nomadnet
timeout 5
start "MeshChat" cmd /k meshchat
```

---

## macOS Setup

### Step 1: Install Homebrew (if not already installed)

Homebrew is a package manager for macOS:

```bash
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
```

### Step 2: Install Python

```bash
brew install python@3.11
```

Verify installation:
```bash
python3 --version
```
```bash
pip3 --version
```

### Step 3: Install Development Tools

```bash
xcode-select --install
```

Click "Install" when prompted.

### Step 4: Install Reticulum

```bash
pip3 install rns
```

Verify installation:
```bash
rnsd --version
```

### Step 5: Install NomadNet

```bash
pip3 install nomadnet
```

Verify installation:
```bash
nomadnet --version
```

### Step 6: Install MeshChat

```bash
pip3 install meshchat
```

Verify installation:
```bash
meshchat --version
```

### Step 7: Initialize Configuration

```bash
# Initialize Reticulum (creates ~/.reticulum/)
rnsd --version
```

```bash
# Initialize NomadNet (creates ~/.nomadnet/)
nomadnet --daemon
```

### Step 8: Start Services

**Terminal 1 - Start Reticulum:**
```bash
rnsd
```

**Terminal 2 - Start NomadNet:**
```bash
nomadnet
```

**Terminal 3 - Start MeshChat:**
```bash
meshchat
```

### Optional: Create Launch Agents

To run services automatically at login, create launch agents.

**Create ~/Library/LaunchAgents/com.reticulum.rnsd.plist:**
```bash
cat > ~/Library/LaunchAgents/com.reticulum.rnsd.plist << 'EOF'
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE plist PUBLIC "-//Apple//DTD PLIST 1.0//EN" "http://www.apple.com/DTDs/PropertyList-1.0.dtd">
<plist version="1.0">
<dict>
    <key>Label</key>
    <string>com.reticulum.rnsd</string>
    <key>ProgramArguments</key>
    <array>
        <string>/usr/local/bin/rnsd</string>
    </array>
    <key>RunAtLoad</key>
    <true/>
    <key>KeepAlive</key>
    <true/>
</dict>
</plist>
EOF
```

Load the agent:
```bash
launchctl load ~/Library/LaunchAgents/com.reticulum.rnsd.plist
```

---

## Linux Setup

These instructions work for Ubuntu, Debian, and Debian-based distributions. Commands for other distributions are provided where different.

### Step 1: Update System

**Ubuntu/Debian:**
```bash
sudo apt update && sudo apt upgrade -y
```

**Fedora:**
```bash
sudo dnf update -y
```

**Arch Linux:**
```bash
sudo pacman -Syu
```

### Step 2: Install Python and pip

**Ubuntu/Debian:**
```bash
sudo apt install python3 python3-pip python3-dev build-essential -y
```

**Fedora:**
```bash
sudo dnf install python3 python3-pip python3-devel gcc -y
```

**Arch Linux:**
```bash
sudo pacman -S python python-pip base-devel
```

Verify installation:
```bash
python3 --version
```
```bash
pip3 --version
```

### Step 3: Install System Dependencies

**Ubuntu/Debian:**
```bash
sudo apt install libssl-dev libffi-dev -y
```

**Fedora:**
```bash
sudo dnf install openssl-devel libffi-devel -y
```

**Arch Linux:**
```bash
sudo pacman -S openssl
```

### Step 4: Install Reticulum

```bash
pip3 install rns
```

If you get a "externally-managed-environment" error on newer systems:
```bash
pip3 install --break-system-packages rns
```

Or create a virtual environment:
```bash
python3 -m venv ~/reticulum-env
source ~/reticulum-env/bin/activate
pip install rns
```

Verify installation:
```bash
rnsd --version
```

### Step 5: Install NomadNet

```bash
pip3 install nomadnet
```

Verify installation:
```bash
nomadnet --version
```

### Step 6: Install MeshChat

```bash
pip3 install meshchat
```

Verify installation:
```bash
meshchat --version
```

### Step 7: Initialize Configuration

```bash
# Initialize Reticulum (creates ~/.reticulum/)
rnsd --version
```

```bash
# Initialize NomadNet (creates ~/.nomadnet/)
nomadnet --daemon
```

### Step 8: Start Services

**Terminal 1 - Start Reticulum:**
```bash
rnsd
```

**Terminal 2 - Start NomadNet:**
```bash
nomadnet
```

**Terminal 3 - Start MeshChat:**
```bash
meshchat
```

### Optional: Create systemd Services

Run services automatically at boot.

**Create /etc/systemd/system/reticulum.service:**
```bash
sudo tee /etc/systemd/system/reticulum.service > /dev/null << 'EOF'
[Unit]
Description=Reticulum Network Stack
After=network.target

[Service]
Type=simple
User=YOUR_USERNAME
ExecStart=/usr/local/bin/rnsd
Restart=on-failure
RestartSec=10

[Install]
WantedBy=multi-user.target
EOF
```

Replace `YOUR_USERNAME` with your actual username:
```bash
sudo sed -i "s/YOUR_USERNAME/$USER/g" /etc/systemd/system/reticulum.service
```

Enable and start:
```bash
sudo systemctl daemon-reload
sudo systemctl enable reticulum.service
sudo systemctl start reticulum.service
```

Check status:
```bash
sudo systemctl status reticulum.service
```

---

## Raspberry Pi Setup

### Step 1: Flash Raspberry Pi OS

1. **Download Raspberry Pi Imager**: [raspberrypi.com/software](https://www.raspberrypi.com/software/)
2. **Flash OS**:
   - Insert SD card
   - Open Raspberry Pi Imager
   - Choose "Raspberry Pi OS (64-bit)" recommended
   - Select your SD card
   - Click settings gear icon (Advanced options)
   - **Enable SSH** (very important!)
   - Set username and password
   - Configure WiFi (if needed)
   - Click "Write"

### Step 2: Boot and Connect

**Option A: Direct connection** (keyboard, mouse, monitor)
- Insert SD card and power on
- Login with credentials you set

**Option B: Headless SSH connection**

1. Insert SD card and power on the Pi
2. Find Pi's IP address on your router or use:
   ```bash
   ping raspberrypi.local
   ```

3. **Connect via SSH from your computer:**

   **From Windows (PowerShell):**
   ```powershell
   ssh pi@raspberrypi.local
   ```
   or
   ```powershell
   ssh pi@192.168.1.XXX
   ```

   **From macOS/Linux:**
   ```bash
   ssh pi@raspberrypi.local
   ```
   or
   ```bash
   ssh pi@192.168.1.XXX
   ```

   Default password is what you set during imaging, or `raspberry` if you didn't change it.

### Step 3: Update System

Once connected to your Pi:

```bash
sudo apt update && sudo apt upgrade -y
```

This may take 10-15 minutes.

### Step 4: Install Python and Dependencies

```bash
sudo apt install python3 python3-pip python3-dev build-essential libssl-dev libffi-dev git -y
```

Verify:
```bash
python3 --version
```

### Step 5: Install Reticulum

```bash
pip3 install rns
```

Add pip install location to PATH:
```bash
echo 'export PATH="$HOME/.local/bin:$PATH"' >> ~/.bashrc
source ~/.bashrc
```

Verify:
```bash
rnsd --version
```

### Step 6: Install NomadNet

```bash
pip3 install nomadnet
```

Verify:
```bash
nomadnet --version
```

### Step 7: Install MeshChat

```bash
pip3 install meshchat
```

Verify:
```bash
meshchat --version
```

### Step 8: Initialize Configuration

```bash
# Initialize Reticulum
rnsd --version
```

This creates `~/.reticulum/`

```bash
# Initialize NomadNet
nomadnet --daemon
```

This creates `~/.nomadnet/`

### Step 9: Configure for Headless Operation

Create systemd service for automatic startup:

```bash
sudo tee /etc/systemd/system/reticulum.service > /dev/null << 'EOF'
[Unit]
Description=Reticulum Network Stack
After=network.target

[Service]
Type=simple
User=pi
ExecStart=/home/pi/.local/bin/rnsd
Restart=on-failure
RestartSec=10

[Install]
WantedBy=multi-user.target
EOF
```

Enable and start:
```bash
sudo systemctl daemon-reload
sudo systemctl enable reticulum.service
sudo systemctl start reticulum.service
```

Check status:
```bash
sudo systemctl status reticulum.service
```

### Step 10: Configure Hardware (LoRa, RNode, etc.)

The Reticulum configuration file is at `~/.reticulum/config`

Edit it:
```bash
nano ~/.reticulum/config
```

**Example for RNode device:**
```ini
[interfaces]
  [[RNode Interface]]
    type = RNodeInterface
    enabled = yes
    port = /dev/ttyUSB0
    frequency = 867200000
    bandwidth = 125000
    txpower = 7
    spreadingfactor = 8
    codingrate = 5
```

**Find your USB device:**
```bash
ls /dev/ttyUSB*
```
or
```bash
ls /dev/ttyACM*
```

Save and restart:
```bash
sudo systemctl restart reticulum.service
```

---

## Security Best Practices

### 1. Secure SSH Access (Raspberry Pi & Linux Servers)

#### Change Default Password

**Immediately change the default password:**
```bash
passwd
```

#### Use SSH Keys Instead of Passwords

**On your local computer (Windows/macOS/Linux), generate SSH key:**

**macOS/Linux:**
```bash
ssh-keygen -t ed25519 -C "your_email@example.com"
```

**Windows (PowerShell):**
```powershell
ssh-keygen -t ed25519 -C "your_email@example.com"
```

Press Enter to accept default location, set a passphrase (recommended).

**Copy key to Pi:**

**macOS/Linux:**
```bash
ssh-copy-id pi@raspberrypi.local
```

**Windows:**
```powershell
type $env:USERPROFILE\.ssh\id_ed25519.pub | ssh pi@raspberrypi.local "cat >> ~/.ssh/authorized_keys"
```

**Test SSH key login:**
```bash
ssh pi@raspberrypi.local
```

You should login without password (or with key passphrase).

#### Disable Password Authentication

**On the Raspberry Pi/Linux server:**
```bash
sudo nano /etc/ssh/sshd_config
```

Find and change these lines:
```
PasswordAuthentication no
ChallengeResponseAuthentication no
PermitRootLogin no
```

Restart SSH:
```bash
sudo systemctl restart ssh
```

#### Change SSH Port (Optional but Recommended)

```bash
sudo nano /etc/ssh/sshd_config
```

Change:
```
Port 22
```
To:
```
Port 2222
```
(or any port between 1024-65535)

Restart SSH:
```bash
sudo systemctl restart ssh
```

Connect with new port:
```bash
ssh -p 2222 pi@raspberrypi.local
```

### 2. Firewall Configuration

#### Linux/Raspberry Pi (UFW)

**Install and enable firewall:**
```bash
sudo apt install ufw -y
```

**Allow SSH (important - do this first!):**
```bash
sudo ufw allow 22/tcp
```

Or if you changed SSH port:
```bash
sudo ufw allow 2222/tcp
```

**Enable firewall:**
```bash
sudo ufw enable
```

**Check status:**
```bash
sudo ufw status
```

**Allow specific ports for Reticulum if needed:**
```bash
sudo ufw allow 4242/udp
```

#### Windows Firewall

Windows Defender Firewall is enabled by default. To allow specific applications:

```powershell
# Allow Python through firewall (run as Administrator)
New-NetFirewallRule -DisplayName "Python" -Direction Inbound -Program "C:\Program Files\Python311\python.exe" -Action Allow
```

#### macOS Firewall

1. Go to System Preferences → Security & Privacy → Firewall
2. Click "Turn On Firewall"
3. Click "Firewall Options"
4. Add Python to allowed applications

### 3. Keep Software Updated

#### Raspberry Pi/Linux

**Enable automatic security updates:**

**Ubuntu/Debian:**
```bash
sudo apt install unattended-upgrades -y
sudo dpkg-reconfigure --priority=low unattended-upgrades
```

**Manual updates (run regularly):**
```bash
sudo apt update && sudo apt upgrade -y
```

#### Windows

Keep Windows Update enabled and automatic.

#### macOS

Enable automatic updates in System Preferences → Software Update.

#### Python Packages

**Check for updates:**
```bash
pip3 list --outdated
```

**Update specific package:**
```bash
pip3 install --upgrade rns
pip3 install --upgrade nomadnet
pip3 install --upgrade meshchat
```

### 4. Reticulum Security Settings

#### Use Encryption

Reticulum uses encryption by default. Verify in `~/.reticulum/config`:

```ini
[reticulum]
  enable_transport = yes
  share_instance = yes
  shared_instance_port = 37428
  instance_control_port = 37429

  # Security settings
  enable_transport = yes
  enable_local_echo = no
```

#### Identity Security

Your Reticulum identity is stored at `~/.reticulum/identities/`

**Backup your identity:**

**Linux/macOS/Raspberry Pi:**
```bash
cp -r ~/.reticulum/identities ~/reticulum_identity_backup
```

**Windows:**
```powershell
Copy-Item -Path "$env:USERPROFILE\.reticulum\identities" -Destination "$env:USERPROFILE\reticulum_identity_backup" -Recurse
```

**Secure the backup:**
```bash
chmod 600 ~/reticulum_identity_backup/*
```

#### Set Proper Permissions

**Linux/macOS/Raspberry Pi:**
```bash
chmod 700 ~/.reticulum
chmod 700 ~/.nomadnet
chmod 600 ~/.reticulum/config
chmod 600 ~/.nomadnet/config
```

### 5. Network Security

#### Use VPN When Accessing Mesh Remotely

Consider using WireGuard or Tailscale for secure remote access.

#### Limit Exposure

Don't expose Reticulum ports directly to the internet unless necessary. Use:
- Port forwarding only when needed
- VPN for remote access
- Local network isolation

### 6. Monitor System Logs

#### Check Reticulum Logs

```bash
journalctl -u reticulum.service -f
```

#### Check SSH Login Attempts (Linux/Pi)

```bash
sudo grep "Failed password" /var/log/auth.log
```

#### Install Fail2Ban (Optional but Recommended)

**Raspberry Pi/Linux:**
```bash
sudo apt install fail2ban -y
sudo systemctl enable fail2ban
sudo systemctl start fail2ban
```

This automatically bans IPs with multiple failed SSH attempts.

### 7. Security Checklist

- [ ] Changed default passwords
- [ ] Using SSH keys instead of passwords
- [ ] Disabled password authentication in SSH
- [ ] Firewall enabled and configured
- [ ] System updates enabled/regular
- [ ] Reticulum identities backed up
- [ ] Proper file permissions set
- [ ] Non-standard SSH port (optional)
- [ ] Fail2Ban installed (servers)
- [ ] VPN configured for remote access (optional)

---

## Troubleshooting

### Common Issues

#### "pip: command not found"

**Solution:**
- Try `pip3` instead of `pip`
- On Windows, ensure Python is in PATH
- Reinstall Python with "Add to PATH" checked

#### "Permission denied" when installing packages

**Linux/macOS:**
```bash
pip3 install --user rns
```

Or use virtual environment (recommended):
```bash
python3 -m venv ~/mesh-env
source ~/mesh-env/bin/activate
pip install rns nomadnet meshchat
```

**Windows (run PowerShell as Administrator):**
```powershell
pip install rns
```

#### "externally-managed-environment" error

**Modern Debian/Ubuntu systems:**
```bash
pip3 install --break-system-packages rns
```

Or use virtual environment (better):
```bash
python3 -m venv ~/mesh-env
source ~/mesh-env/bin/activate
pip install rns nomadnet meshchat
```

#### Cannot find USB device

**Check connected devices:**

**Linux/Pi:**
```bash
ls /dev/ttyUSB*
ls /dev/ttyACM*
dmesg | grep tty
```

**Add user to dialout group:**
```bash
sudo usermod -a -G dialout $USER
```

Log out and back in for changes to take effect.

**macOS:**
```bash
ls /dev/cu.*
```

**Windows:**
Check Device Manager → Ports (COM & LPT)

#### Reticulum won't start

**Check logs:**
```bash
rnsd -vvv
```

**Check configuration:**
```bash
nano ~/.reticulum/config
```

Look for syntax errors or invalid interface settings.

#### NomadNet connection issues

**Verify Reticulum is running:**
```bash
ps aux | grep rnsd
```

**Check interface status:**
```bash
rnstatus
```

#### SSH connection refused

**Check SSH service:**
```bash
sudo systemctl status ssh
```

**Restart SSH:**
```bash
sudo systemctl restart ssh
```

**Check firewall:**
```bash
sudo ufw status
```

#### Can't connect to Raspberry Pi

**Check Pi is on network:**
```bash
ping raspberrypi.local
```

**Find Pi IP address on router admin page**

**Check SSH is enabled:**
- Re-flash SD card with SSH enabled in Raspberry Pi Imager

### Getting Help

#### Official Documentation

- **Reticulum**: [github.com/markqvist/Reticulum](https://github.com/markqvist/Reticulum)
- **NomadNet**: [github.com/markqvist/NomadNet](https://github.com/markqvist/NomadNet)
- **MeshChat**: Check project repository

#### Community Support

- GitHub Issues on respective repositories
- Reticulum Matrix channel
- Community forums

#### Log Files Location

**Linux/macOS/Pi:**
- Reticulum: `~/.reticulum/logfile`
- NomadNet: `~/.nomadnet/logfile`
- System logs: `/var/log/syslog` or `journalctl`

**Windows:**
- Reticulum: `%USERPROFILE%\.reticulum\logfile`
- NomadNet: `%USERPROFILE%\.nomadnet\logfile`

---

## Next Steps

After completing setup:

1. **Join the Network**: Connect to other Reticulum nodes
2. **Configure Interfaces**: Set up your radio hardware
3. **Explore NomadNet**: Browse pages and connect with others
4. **Try MeshChat**: Start communicating over the mesh
5. **Build Your Node**: Set up a permanent node or portable station
6. **Contribute**: Help grow the network and contribute to projects

---

## Additional Resources

### Hardware Guides
- **Building an RNode**: [unsigned.io/rnode](https://unsigned.io/rnode)
- **LoRa Module Setup**: Check manufacturer documentation
- **Raspberry Pi Projects**: [raspberrypi.com/documentation](https://www.raspberrypi.com/documentation/)

### Configuration Examples
Located in `~/.reticulum/config` after first run. Examples include:
- TCP interfaces for internet connectivity
- AutoInterface for automatic local discovery
- RNode for LoRa radio
- Serial modem configurations

### Performance Tuning
- Adjust Reticulum interface parameters for your hardware
- Optimize bandwidth and spreading factor for range vs. speed
- Configure multiple interfaces for redundancy

---

**Document Version**: 1.0
**Last Updated**: 2025-11-04
**License**: Public Domain / CC0

For issues or improvements to this guide, please open an issue in the repository.
