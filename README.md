

# Unity APK to Quest Fleet via ADB & FTP

🚧 **UNDER CONSTRUCTION** 🚧

I'm using Shadow Tech and need to seamlessly publish APKs to several Quest 3 headsets or phones located near a Raspberry Pi 5 running ADB.

I also want all devices to automatically connect to Wi-Fi when plugged in, making it easy for non-IT users to operate on the Pi side.

The goal is to quickly iterate Unity3D builds and test them on four Quest headsets **without repeating all the manual steps** for each update.

---

## Requirements

- A computer to build the game
- An FTP server accessible by both the computer and the Raspberry Pi(s)
- A Raspberry Pi with ADB installed

---

## Workflow (Step by Step)

### Editor Side (Unity3D Machine)
- Build the APK using Unity3D
- Use a Python script to push the APK and a `namespace` info file to the FTP server (hosted on the Pi)
  - This can be done manually or automatically (e.g. script checks for new builds every 5 seconds)

### Raspberry Pi (LAN Side)
- Periodically (e.g. every 5 seconds), the Pi checks the FTP server for new builds
- If a new APK is found, it installs it via ADB to the connected devices

---

## How to Install an FTP Server on a Raspberry Pi

```bash
sudo apt update
sudo apt full-upgrade
sudo apt install vsftpd -y
sudo nano /etc/vsftpd.conf
```

Recommended `vsftpd.conf` configuration:

```conf
anonymous_enable=YES
local_enable=YES
write_enable=YES
anon_upload_enable=NO
anon_mkdir_write_enable=NO
anon_other_write_enable=NO
dirmessage_enable=YES
use_localtime=YES
xferlog_enable=YES
connect_from_port_20=YES
listen=NO
listen_ipv6=YES
local_root=/ftp/
```

Then, create and set permissions on the FTP root:

```bash
sudo mkdir -p /ftp
sudo chmod 755 /ftp
```

---

🎥 Reference Video: [YouTube Link (starts at 1:24)](https://youtu.be/Kf1U1bG9d2A?t=84)
