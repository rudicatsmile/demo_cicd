# 02 - Networking dan IP Static

## Cek Informasi Jaringan

```bash
# Cara klasik
ifconfig

# Cara modern
ip a
ip addr show

# Lihat routing table
ip route
route -n
```

---

## Konfigurasi IP Static dengan Netplan (Ubuntu modern)

File konfigurasi biasanya berada di:

```bash
sudo nano /etc/netplan/01-netcfg.yaml
# atau
sudo nano /etc/netplan/00-installer-config.yaml
```

### Contoh konfigurasi Static

```yaml
network:
  version: 2
  renderer: networkd
  ethernets:
    enp0s3:                     # Ganti sesuai nama interface Anda
      dhcp4: no
      addresses:
        - 192.168.1.221/24
      gateway4: 192.168.1.1
      nameservers:
        addresses: [8.8.8.8, 1.1.1.1]
```

### Terapkan konfigurasi

```bash
sudo netplan apply
# atau untuk testing dulu
sudo netplan try
```

### Contoh lain dari latihan (VirtualBox)

```yaml
network:
  ethernets:
    enp0s3:
      dhcp4: no
      addresses: [192.168.1.200/24]
      gateway4: 192.168.1.1
  version: 2
```

---

## Konfigurasi dengan `/etc/network/interfaces` (cara lama)

Edit file:

```bash
sudo nano /etc/network/interfaces
# atau
sudo vim /etc/network/interfaces
```

### 1. DHCP

```bash
# The loopback network interface
auto lo
iface lo inet loopback

# The primary network interface
auto eth0
iface eth0 inet dhcp

auto eth1
iface eth1 inet static
  address 172.21.100.1
  netmask 255.255.255.0
```

### 2. Static

```bash
# The loopback network interface
auto lo
iface lo inet loopback

# The primary network interface
auto eth0
iface eth0 inet static
  address 192.168.0.2
  netmask 255.255.255.0
  gateway 192.168.0.1
  dns-nameservers 180.131.144.144 180.131.155.155

auto eth1
iface eth1 inet static
  address 172.21.100.1
  netmask 255.255.255.0
```

### Restart networking

```bash
sudo service networking restart
# atau
sudo systemctl restart networking
```

---

## Transfer File antar Host (SCP)

```bash
# Copy folder secara rekursif ke remote host
scp -r /home/rudi/sekolah-hacker/ rudi@192.168.1.4:"/home/rudi/transfer"
```

Penjelasan:
- `-r` = recursive (folder + isinya)
- `rudi@192.168.1.4` = user dan IP tujuan
- `"/home/rudi/transfer"` = path tujuan di remote (gunakan tanda kutip jika ada spasi)

---

## Reset Password Ubuntu di VirtualBox (Recovery Mode)

Jika lupa password:

1. Restart VM
2. Tekan `Ctrl + F12` (atau `Esc` / `Shift`) saat boot
3. Pilih **Advanced options** → pilih kernel yang ada tulisan **recovery**
4. Pilih **root - Drop to root shell prompt**
5. Di prompt root:

```bash
ls /home                  # Lihat nama user (contoh: hacker)
passwd hacker             # Ganti password user tersebut
```

6. Ketik password baru dua kali, lalu reboot.

---

## Catatan Penting

- Nama interface (`enp0s3`, `eth0`, `ens33`, dll.) berbeda di setiap mesin. Cek dulu dengan `ip a` atau `ifconfig`.
- Setelah mengubah Netplan, selalu jalankan `sudo netplan apply`.
- `gateway4` sudah deprecated di Netplan versi baru. Versi terbaru lebih disarankan menggunakan:

```yaml
routes:
  - to: default
    via: 192.168.1.1
```

- File `/etc/hosts` juga sering diedit untuk testing domain lokal (contoh multiple domain Nginx).

---

## Referensi

- Dokumentasi resmi Netplan: https://netplan.io/
- Ubuntu Server Guide - Networking
