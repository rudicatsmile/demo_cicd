# Catatan Pentest & Security for everyone

Struktur catatan hasil rapi dari materi Sekolah Hacker / Cilsy (`latihan3.txt`).

Fokus: **belajar terstruktur, lab berizin, dokumentasi aman**.  
Jangan simpan API key, password, token, atau data klien di folder ini.

---

## Cara pakai

1. Baca file berurutan mengikuti **Alur belajar** di bawah, atau loncat sesuai kebutuhan.
2. Gunakan heading `##` / `###` agar outline di editor tetap rapi.
3. Perintah lab taruh di code block:
   ````markdown
   ```bash
   perintah-di-sini
   ```
   ````
4. Setiap selesai lab, isi template di `99-Lab-dan-Exercise.md`.
5. Sebelum commit Git / share: pastikan tidak ada secret.

**Editor yang disarankan:** Obsidian, VS Code (+ Markdown Preview), Typora.

---

## Alur belajar (disarankan)

```text
00 Overview & metodologi
    ↓
01–05  Linux, network, user, paket, hardening
    ↓
06–08  Recon → Nmap → vulnerability scanning
    ↓
09     Web vulnerabilities (XSS, SQLi, CSRF, auth, misconfig)
    ↓
10–11  Metasploit (konsep lab) + Burp Suite
    ↓
12     Mobile security
    ↓
13–14  Tools pendukung + resources
    ↓
99     Latihan & jurnal lab
```

---

## Daftar isi induk

### Fondasi & metodologi

| File | Isi utama |
|------|-----------|
| [00-Overview-dan-Metodologi.md](00-Overview-dan-Metodologi.md) | Tujuan pentest, blackbox/whitebox/greybox, alur PTES-style, timeline, isi laporan, rules of engagement, etika |

### Sistem Linux & infrastruktur

| File | Isi utama |
|------|-----------|
| [01-Linux-Fundamentals.md](01-Linux-Fundamentals.md) | Shortcut Bash, alias, perintah dasar, archive tar/gzip, `find`, grep/cut/sed |
| [02-Networking-dan-IP-Static.md](02-Networking-dan-IP-Static.md) | `ip`/`ifconfig`, Netplan, `/etc/network/interfaces`, SCP, recovery password VM |
| [03-User-Group-Permission-SUID.md](03-User-Group-Permission-SUID.md) | User/group, `/etc/passwd` & shadow, permission, SUID, cron |
| [04-Package-Management-dan-Services.md](04-Package-Management-dan-Services.md) | APT, `.deb`, systemctl, Nginx + PHP, multiple virtual host |
| [05-Hardening-Lynis.md](05-Hardening-Lynis.md) | Install/update Lynis, audit lokal/remote/Dockerfile, tips hardening |

### Recon & scanning

| File | Isi utama |
|------|-----------|
| [06-Recon-Passive-Active.md](06-Recon-Passive-Active.md) | Passive vs active, theHarvester, Dmitry, Sudomy, DNS tools, Shodan (query contoh), Recon-ng, Spiderfoot, proxychains |
| [07-Nmap-Cheat-Sheet.md](07-Nmap-Cheat-Sheet.md) | Target syntax, scan types, timing, OS detect, NSE/vulners, output formats |
| [08-Vulnerability-Scanning.md](08-Vulnerability-Scanning.md) | Nessus, Nmap scripts, Nikto, ZAP, WMap, Rapidscan, WPScan, SAST tools, CVE/CWE/CVSS |

### Kerentanan web

Folder: [09-Web-Vulnerabilities/](09-Web-Vulnerabilities/)

| File | Isi utama |
|------|-----------|
| [XSS.md](09-Web-Vulnerabilities/XSS.md) | Jenis XSS, dampak, penyebab, mitigasi, lab PortSwigger/DVWA |
| [SQL-Injection.md](09-Web-Vulnerabilities/SQL-Injection.md) | Jenis SQLi, SQLMap di lab, mitigasi parameterized query, DVWA |
| [CSRF.md](09-Web-Vulnerabilities/CSRF.md) | Konsep CSRF, dampak, token/SameSite, lab |
| [Broken-Auth.md](09-Web-Vulnerabilities/Broken-Auth.md) | Session & login flaws, checklist uji berizin, mitigasi |
| [Misconfiguration.md](09-Web-Vulnerabilities/Misconfiguration.md) | Directory listing, `.git`, default config, header, hardening |

### Framework, proxy, mobile, tools

| File | Isi utama |
|------|-----------|
| [10-Metasploit-dan-Post-Exploitation.md](10-Metasploit-dan-Post-Exploitation.md) | msfdb, workspace, alur `search/use/info/options`, konsep post-exploitation di lab |
| [11-Burp-Suite.md](11-Burp-Suite.md) | Proxy, certificate, Repeater, Intruder, alur kerja lab web |
| [12-Mobile-Security.md](12-Mobile-Security.md) | ADB, storage app, jadx/MobSF, konsep Frida/Objection, MSTG/MASVS |
| [13-Tools-Lain.md](13-Tools-Lain.md) | Ngrok, Gobuster, fuzzing (konsep), auth testing lab, Tor/proxychains, batasan tool SE |
| [14-Resources-dan-Cheat-Sheet.md](14-Resources-dan-Cheat-Sheet.md) | Platform lab, OWASP/PTES/CVSS, SecLists, sumber OSINT, daftar yang tidak boleh disimpan |

### Jurnal latihan

| File | Isi utama |
|------|-----------|
| [99-Lab-dan-Exercise.md](99-Lab-dan-Exercise.md) | DVWA Docker, PortSwigger, HTB/THM/VulnHub, template catatan lab, TODO, etika |

---

## Peta cepat “mau apa → buka file mana”

| Kebutuhan | Buka |
|-----------|------|
| Baru mulai, pahami proses pentest | `00-Overview-dan-Metodologi.md` |
| Command Linux sehari-hari | `01-Linux-Fundamentals.md` |
| IP static / Netplan | `02-Networking-dan-IP-Static.md` |
| User, SUID, cron | `03-User-Group-Permission-SUID.md` |
| Nginx + PHP | `04-Package-Management-dan-Services.md` |
| Audit hardening | `05-Hardening-Lynis.md` |
| OSINT / DNS / Shodan | `06-Recon-Passive-Active.md` |
| Opsi Nmap | `07-Nmap-Cheat-Sheet.md` |
| Scanner & SAST | `08-Vulnerability-Scanning.md` |
| XSS / SQLi / CSRF / Auth | folder `09-Web-Vulnerabilities/` |
| msfconsole | `10-Metasploit-dan-Post-Exploitation.md` |
| Intercept HTTP | `11-Burp-Suite.md` |
| Android lab | `12-Mobile-Security.md` |
| Gobuster, Ngrok, dll. | `13-Tools-Lain.md` |
| Link & standar | `14-Resources-dan-Cheat-Sheet.md` |
| Catat progress lab | `99-Lab-dan-Exercise.md` |

---

## Konvensi penulisan di repo ini

- Bahasa: Indonesia + istilah teknis Inggris yang umum
- Perintah: selalu di fenced code block
- Target contoh: `lab-lokal`, IP dokumentasi, atau mesin HTB/THM—bukan domain produksi acak
- Temuan: cantumkan dampak + mitigasi, bukan hanya “vulnerable”
- Secret: **dilarang** (API key, password, activation code, token Ngrok, cookie sesi nyata)

---

## Status kelengkapan

| Area | Status |
|------|--------|
| 00–08 Fondasi & scanning | Lengkap (template terisi) |
| 09 Web vulnerabilities | Lengkap (5 topik) |
| 10–14 Tools & resources | Lengkap |
| 99 Lab journal | Lengkap (siap diisi progress pribadi) |

---

## Tips Obsidian (opsional)

- Tag contoh di frontmatter atau baris atas: `#linux` `#web` `#mobile` `#lab`
- Link antar catatan: `[[07-Nmap-Cheat-Sheet]]`
- Graph view membantu melihat hubungan topik

---

## Pengingat etika

Catatan ini untuk **pembelajaran dan pengujian berizin**.  
Lab (DVWA, PortSwigger, HTB, THM, VulnHub, VM sendiri) ≠ izin menguji sistem pihak ketiga tanpa kontrak atau program bug bounty yang jelas scopenya.
