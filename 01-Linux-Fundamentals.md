# 01 - Linux Fundamentals

## Keyboard Shortcuts (Bash)

| Shortcut   | Fungsi                              |
|------------|-------------------------------------|
| `Ctrl + U` | Hapus satu baris                    |
| `Ctrl + W` | Hapus satu kata sebelum cursor      |
| `Ctrl + K` | Hapus dari cursor sampai akhir baris|
| `Ctrl + A` | Pindah ke awal baris                |
| `Ctrl + E` | Pindah ke akhir baris               |
| `Ctrl + Y` | Yank / Undo (paste yang dihapus)    |
| `Ctrl + L` | Clear screen (bersihkan layar)      |
| `Ctrl + R` | Search history perintah             |

---

## Alias

Edit file `~/.bashrc`:

```bash
nano ~/.bashrc
```

Contoh isi alias yang berguna:

```bash
alias ruru='cd /home/rudi/sekolah_hacker'
alias ic='ifconfig'
alias sagi='sudo apt-get install'
alias sagu='sudo apt-get update'
```

Aktifkan perubahan:

```bash
source ~/.bashrc
```

Setelah itu, mengetik `ic` akan sama dengan menjalankan `ifconfig`.

---

## Perintah Dasar

```bash
# Lihat user yang sedang login
w

# Hapus folder beserta isinya (HATI-HATI!)
rm -rf nama_folder

# Lihat penggunaan Memory
free -h

# Lihat penggunaan Disk
df -h

# Buat folder beserta subfolder
mkdir -p data03/script

# Copy folder beserta isinya
cp -r folder1 data02/

# Rename file
mv file1 file2

# Pindahkan file ke folder lain
mv file1 data02/

# Buat symbolic link (shortcut)
ln -s /home/rudi/hello.sh hello_symbolic.sh

# Copy file/folder antar host (SCP)
scp -r /home/rudi/sekolah-hacker/ rudi@192.168.1.4:"/home/rudi/transfer"

# Lihat proses tertentu (contoh: mysql)
ps aux | grep mysql

# Tampilkan history tanpa nomor baris
history | cut -c 8-
```

---

## Archive (tar, gzip, bzip2, xz)

### Membuat archive

```bash
# Buat beberapa file sekaligus untuk latihan
touch kompres_file{0..9}

# tar.gz
tar czf filesaya.tar.gz kompres_file{0..9}

# tar.bz2
tar cjf filesaya.tar.bz2 kompres_file{0..9}

# tar.xz
tar cJf filesaya.tar.xz kompres_file{0..9}
```

### Melihat isi archive

```bash
tar tvf filesaya.tar.gz
tar tf filesaya.tar.gz          # versi singkat
```

### Extract / Dekompres

```bash
# Extract tar.gz
tar xzf filesaya.tar.gz

# Extract dengan gzip (file asli .gz akan hilang)
gzip -d filesaya.tar.gz
gunzip ip.txt.gz
```

### Contoh praktis dari latihan

```bash
mkdir kompresi
ifconfig > ip.txt
tar -cvzf ip.tar.gz ip.txt
rm ip.txt

# Extract kembali
tar -xvzf ip.tar.gz
cat ip.txt
```

---

## Finding File

```bash
# Cari semua file .conf di /etc (case-insensitive)
find /etc -iname "*.conf" -print

# Cari file biasa berukuran > 2MB, maksimal 3 level folder
find . -maxdepth 3 -type f -size +2M -print

# Cari file .conf yang dimodifikasi dalam 180 hari terakhir
find /etc -iname "*.conf" -mtime -180 -print

# Cari file dengan permission 777
find /home/user -perm 777
```

---

## Filter & Manipulasi Teks (grep, cut, sed, sort)

### Contoh 1 – Filter baris yang dimulai angka + mengandung "cilsy" + diakhiri @

```bash
grep -E '^[0-9]' latihan2.txt | grep 'cilsy' | grep -v '[0-9][0-9]' | grep -E '@$' > latihan1-3.txt
```

### Contoh 2 – Ambil IP dari output ifconfig lalu ganti titik menjadi strip

```bash
cat latihan3.txt | grep 'inet addr' | cut -d: -f2 | cut -d' ' -f1 | sort | sed 's/\./-/g'
```

Penjelasan singkat:

1. `grep 'inet addr'` → ambil baris yang mengandung "inet addr"
2. `cut -d: -f2` → potong berdasarkan `:` ambil field ke-2
3. `cut -d' ' -f1` → potong berdasarkan spasi ambil field pertama
4. `sort` → urutkan
5. `sed 's/\./-/g'` → ganti semua titik menjadi tanda strip

### Perintah sed & cut yang sering dipakai

```bash
# Potong karakter 1 sampai 3
cut -b 1-3 filetest.txt

# Ganti kata (case sensitive)
sed 's/rizal/cilsy/g' filetest.txt

# Ganti kata (case insensitive)
sed 's/[rR][iI][zZ][aA][lL]/cilsy/g' filetest.txt

# Hapus baris yang diawali angka 1-9
sed '/^[1-9]/d' filetest.txt

# Hitung kemunculan unik
sort file3.txt | uniq -c
```

---

## Catatan Penting

- Perintah `rm -rf` sangat berbahaya. Pastikan path sudah benar sebelum dijalankan.
- Selalu gunakan `free -h` dan `df -h` (opsi `-h` = human readable).
- Symbolic link (`ln -s`) berbeda dengan hard link. Symbolic link bisa menunjuk ke file/folder di filesystem berbeda.
- Setelah mengedit `.bashrc`, wajib menjalankan `source ~/.bashrc` atau buka terminal baru.

---

## Referensi

- Man page: `man bash`, `man tar`, `man find`, `man sed`
- Cheat sheet Bash yang bagus: [https://devhints.io/bash](https://devhints.io/bash)
