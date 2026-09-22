# 00 - Overview dan Metodologi Pentest

## Deskripsi
Ringkasan cara merencanakan, menjalankan, dan melaporkan penetration testing secara profesional. Materi ini merujuk praktik umum di industri serta catatan kursus (planning → draft report → re-test → final report).

---

## Tujuan pentest
- Mengidentifikasi kelemahan sebelum pihak yang tidak berwenang menemukannya
- Memberi bukti dampak bisnis yang jelas
- Memberi rekomendasi perbaikan yang bisa ditindaklanjuti
- Bukan “hanya mencari bug”, melainkan membantu menurunkan risiko

---

## Blackbox vs Whitebox

| Aspek | Blackbox | Whitebox |
|-------|----------|----------|
| Informasi awal | Minim (URL, IP, scope) | Source code, kredensial, arsitektur, akses internal |
| Sudut pandang | Menyerupai penyerang luar | Lebih dekat ke review keamanan + attacker berpengetahuan |
| Waktu | Sering lebih lama untuk recon | Lebih cepat menemukan root cause di kode/konfigurasi |
| Kelebihan | Realistis terhadap ancaman eksternal | Cakupan dalam lebih baik, cocok untuk SAST + config review |
| Kekurangan | Bisa melewatkan isu logika dalam | Butuh trust & persiapan data dari klien |
| Kebutuhan klien | Scope & rules of engagement | Credential uji, VPN, dokumen, akses repo (sesuai NDA) |

Greybox (informasi sebagian) sering dipakai di praktik: akun user biasa + admin uji, tanpa seluruh source code.

---

## Metodologi umum (alur kerja)

1. **Pre-engagement / Planning**  
   Scope, tujuan, larangan (mis. tidak DoS, tidak ubah data produksi), kontak darurat, jadwal, NDA.

2. **Intelligence gathering (Recon)**  
   Pasif dulu, aktif sesuai izin. Lihat catatan `06-Recon` dan `07-Nmap`.

3. **Vulnerability analysis**  
   Scanner + review manual. Lihat `08-Vulnerability-Scanning`.

4. **Exploitation (hanya dalam scope)**  
   Membuktikan dampak di lingkungan yang disepakati, dengan hati-hati pada data.

5. **Post-exploitation (lab / dengan izin ketat)**  
   Memahami seberapa jauh akses bisa berkembang; dokumentasikan, jangan merusak.

6. **Reporting**  
   Draft → presentasi (jika diminta) → perbaikan klien → **re-test** → final report.

7. **Cleanup**  
   Hapus akun uji, backdoor lab, file temporary, akses VPN yang sudah tidak perlu.

Referensi alur: PTES, OWASP Testing Guide, PCI DSS Penetration Testing Guidance.

---

## Timeline contoh (dari materi kursus)

1. Meeting pentest (planning)
2. Jika whitebox: klien siapkan credential, firewall/VPN, dokumen aplikasi
3. Pelaksanaan pentest (mis. 3–5 hari blackbox, bisa lebih lama)
4. Tim menyusun **draft report**
5. Serahkan draft + presentasi jika diminta
6. Klien memperbaiki temuan (waktu fleksibel)
7. **Re-test** fokus pada temuan sebelumnya
8. Tim menyusun **final report**
9. Penyerahan final report

Catatan instruktur: sebelum tes yang bisa menulis ke database, minta backup. Untuk cek IDOR, idealnya ada minimal 2 user biasa + 1 admin.

---

## Isi laporan yang baik
- Ringkasan eksekutif (bahasa bisnis)
- Scope & metodologi
- Temuan per prioritasi (Critical → Info)
- Bukti (screenshot, request/response yang disamarkan jika perlu)
- Dampak
- Rekomendasi perbaikan
- Hasil re-test
- Lampiran teknis

Gunakan CVE/CWE/CVSS bila relevan (lihat file Resources).

---

## Rules of engagement (poin penting)
- Hanya target yang tertulis di scope
- Tidak menguji sistem pihak ketiga di luar kesepakatan
- Tidak mencuri data nyata; gunakan data uji bila mungkin
- Hentikan tes jika sistem produksi terganggu, lalu hubungi kontak klien
- Simpan bukti secara aman; jangan sebarkan

---

## Kualifikasi & etika
- Kompetensi teknis + komunikasi + dokumentasi
- Hormati hukum setempat dan kontrak
- Bug bounty punya scope sendiri—baca kebijakan program sebelum mulai

Contoh program untuk belajar membaca scope: Bugcrowd (program publik), kebijakan VDP perusahaan.

---

## Standar & referensi
- http://www.pentest-standard.org/ (PTES)
- OWASP Testing Guide / ASVS / Top 10
- PCI DSS Penetration Testing Guidance
- CWE, CVE, CVSS

## Catatan penting
- Scanner ≠ pentest selesai; verifikasi manual tetap wajib
- Re-test adalah bagian dari nilai jasa, bukan opsional
- Jangan menyimpan kredensial klien di catatan pribadi / Git
