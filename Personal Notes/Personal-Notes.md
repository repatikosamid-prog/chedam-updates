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

## Open items / next notes

- Fill in the network record table in `docs/P0-restart-new-network.md` (no passwords).
