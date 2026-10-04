# Chedam — Personal Notes

Problems I've noticed so far while setting up the project, and how I'm handling them.

---

## 1. Hard disk health → switching from a physical DB to DuckDB

*Noted: October 3, 2026*

- **Check first:** Before building on a machine, check the hard drive's health and condition.
- **Tool used:** CrystalDiskInfo, which shows the health status and S.M.A.R.T. readings a drive should be within.
- **Finding:** My HDD is **not in a good state**.
- **Decision:** Replace the plan of running a physical (server-installed) database with a **virtual/embedded database using DuckDB**.

---

## 2. Wi-Fi / router — no admin access on the TELUS modem

*Noted: October 3, 2026*

- **Problem:** We use a TELUS-provided modem with built-in Wi-Fi. We **don't have admin credentials** or authority to change settings such as adding or removing DHCP entries.
- **Workaround:** Added a **separate Wi-Fi router connected by LAN (Ethernet) cable to the wall port in my bedroom**, broadcasting its own Wi-Fi network.
- **Why it works:** I have admin credentials and full control of the new router, so I can manage DHCP and network settings myself.

---

## 3. Restarting the project on the new network

*Noted: October 3, 2026*

- The new router gave everything new IP addresses, and the old Raspberry Pi credentials and setup became confusing.
- **Decision:** Wipe the Pi SD card and restart P0 setup from scratch on the new network, with new IPs and a new Pi password.
- Steps: `docs/P0-restart-new-network.md`.

---

## 4. Pi back online on the new network: SSH keys, wrong key, blank screen

*Noted: October 3, 2026*

- **Result:** Pi Zero 2 W re-flashed and running on the new router's Wi-Fi at 192.168.50.101 (DHCP reservation), key-only SSH, OS updated, console login showing on HDMI.
- **Why keys:** the private key stays on my PC and the Pi only holds the public key, so nothing secret crosses the network and passwords can't be guessed. Password login over SSH is off.
- **Biggest mistake:** Raspberry Pi Imager had remembered an old public key from an earlier session, so the Pi rejected my real key ("Permission denied (publickey)"). Then I pasted a PowerShell command into Imager's key box instead of the key. Fix: REMOVE, then BROWSE to `id_ed25519.pub`, and re-flash.
- **Small traps:** `<old-ip>` style placeholders must be replaced, but `$env:USERPROFILE` must not; Git Bash needs `/` not `\`; after a re-flash the "host identification has changed" warning is normal (`ssh-keygen -R <ip>`); the TP-Link saved the reservation as *Disabled* until I enabled it.
- **Blank screen:** Lite has no desktop by design (512 MB RAM). The screen stayed black until HDMI output was forced in `cmdline.txt`.
- **Git:** first push failed with 403 (saved GitHub login could not write). Clearing the saved login and signing in through the browser fixed it. New clones also needed `git config --global user.name/user.email`.
- Full step-by-step log: `docs/P0-pi-setup-log-2026-10-03.pdf` in the main chedam repo.

---

## Open items / next notes

- ~~Fill in the network record table in `docs/P0-restart-new-network.md`~~ (done 2026-10-03).
- Next: hub setup on the Pi (`setup-hub.sh`).
