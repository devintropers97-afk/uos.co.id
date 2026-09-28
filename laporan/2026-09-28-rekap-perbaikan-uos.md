# Rekap Perbaikan Website uos.co.id — Hari 1

**Klien:** PT Unggulan Operator Sinergis (UOS)
**Pekerjaan:** Perbaikan situs uos.co.id (paket Rp 1.500.000, sesuai proposal SITUNEO 19 Sep 2026, hal. 13)
**Tanggal pengerjaan:** Senin, 28 September 2026
**Dikerjakan oleh:** SITUNEO Digital Solusi Indonesia

---

## 1. Ringkasan Eksekutif

- **Sertifikat keamanan (SSL) aktif kembali** setelah ±120 hari kedaluwarsa. Peringatan "Tidak aman" di browser hilang.
- **Website dibuka kembali untuk Google.** Sebelumnya situs diatur *noindex* (diblokir dari hasil pencarian).
- **Berat gambar turun 87% (hemat 44,75 MB)** lewat konversi ke WebP.
- **Waktu tampil gambar utama di HP turun dari 71,9 detik ke 9,1 detik** (−87%).
- **7 plugin diperbarui**, dan jumlah plugin berstatus *Vulnerable* turun dari 9 ke 6.
- **Konfigurasi server diperbaiki.** Library gambar (GD/Imagick) dan extension `dom` sebelumnya tidak aktif.
- **Temuan kritis (hasil audit database):** **semua link WhatsApp, telepon, dan email di footer (tampil di seluruh halaman) dan di halaman Kontak mengarah ke nomor/email palsu dari template** (`123-456-7890`, `213-200-5078`, `contact@mysite.com`, `kevinclarkfit@training.com`). Pengunjung yang mengklik tidak pernah sampai ke UOS.
- **Formulir Kontak belum pernah menghasilkan calon asli.** Dari 102 kiriman (Jun 2025 – Sep 2026): 3 tes developer, 99 spam. Tidak ada satu pun yang pernah dibuka di WP Admin.
- **Email website gagal sejak Juni 2026** (*Could not connect to SMTP host*), sesuai dengan tanggal SSL kedaluwarsa. Sejak Juni 2025 notifikasi ke `admin@uos.co.id` juga selalu gagal karena **mailbox tersebut tidak ada**.
- **Tidak ditemukan malware.** 3.224 file inti WordPress dan 9 plugin gratis identik dengan versi resmi.

---

## 2. Kondisi Awal (sebelum dikerjakan)

| Area | Temuan |
|---|---|
| SSL | Let's Encrypt kedaluwarsa sejak **31 Mei 2026**. AutoSSL tidak memperpanjang. SSL Sectigo berbayar (aktif s.d. 10 Jul 2027) belum pernah diterbitkan atau dipasang. |
| SEO | Pengaturan WordPress *"Discourage search engines"* aktif → tag `noindex, nofollow` di semua halaman |
| Gambar | Foto halaman depan berformat PNG 1–2,7 MB per file (±22 MB untuk 10 foto terbesar) |
| Server | PHP 8.1 lewat MultiPHP tanpa extension **gd, imagick, dom** → WordPress tidak bisa membuat thumbnail, dan plugin gambar/WPForms error |
| Plugin | 16 plugin, **9 berstatus Vulnerable**, 16 update tertunda, auto-update mati |
| WordPress | Versi 6.7.9 (terbaru 7.1.2) |
| Komentar | 322 komentar pending, semuanya spam berisi link mencurigakan |
| Email | WP Mail SMTP mencatat **12 email gagal** dalam 30 hari terakhir |
| Backup | Backup otomatis terakhir 419 hari lalu |
| Tracking | Belum ada GA4, GTM, Meta Pixel, TikTok Pixel |
| Formulir | Tidak ada formulir di halaman depan, hanya di halaman Kontak |
| Open Graph | Tidak ada `og:image`. Preview link di WhatsApp kosong. |

---

## 3. Pekerjaan yang Sudah Selesai

| # | Pekerjaan | Hasil | Status |
|---|---|---|---|
| 1 | Backup penuh (Softaculous) | File `wp.26_12568.2026-09-28_13-18-04.tar.gz` (263,51 MB), diunduh ke komputer SITUNEO | ✅ |
| 2 | Terbitkan ulang SSL (Let's Encrypt via SSL/TLS Wizard cPanel) | 10 domain/subdomain tervalidasi dan aman: uos.co.id, www, mail, webmail, cpanel, autodiscover, autoconfig, dll. | ✅ |
| 3 | Redirect HTTP → HTTPS dan www → non-www | Sudah berjalan, terverifikasi | ✅ |
| 4 | Buka blokir Google (Settings → Reading) | Tag robots berubah dari `noindex, nofollow` menjadi `max-image-preview:large` | ✅ |
| 5 | Update plugin aman (tahap A) | Backuply, Contact Form 7, Hello Plus, Akismet, WP Mail SMTP, WP Rocket, WPForms Lite | ✅ |
| 6 | Aktifkan PHP Selector 8.1 + extension | gd, imagick, dom, xml, fileinfo, exif, dan extension wajib WordPress. Domain dipindah dari MultiPHP ke PHP Selector (arahan support Rumahweb). | ✅ |
| 7 | Konversi gambar ke WebP (Converter for Media) | 65 gambar dikonversi, **hemat 44,75 MB (87%)**, dikirim lewat .htaccess (URL tidak berubah) | ✅ |
| 8 | Optimasi WP Rocket | Minify CSS/JS, Load JS deferred, Delay JS (Safe Mode), Optimize CSS delivery → *Load CSS asynchronously* | ✅ |

---

## 4. Hasil PageSpeed (Before → After)

Sumber: pagespeed.web.dev. Before: 28 Sep 2026 14:11. After: 28 Sep 2026 17:39.

| Metrik | Mobile Before | Mobile After | Desktop Before | Desktop After |
|---|---|---|---|---|
| Performance | 65 | **69** | 65 | **71** (sempat 80) |
| Largest Contentful Paint | 71,9 dtk | **9,1 dtk** | 9,5 dtk | **4,1 dtk** (sempat 2,1) |
| Speed Index | 36,0 dtk | **6,6 dtk** | 9,5 dtk | **3,2 dtk** |
| Total Blocking Time | 20 ms | **0 ms** | 40 ms | **10 ms** |
| First Contentful Paint | 1,5 dtk | 1,4 dtk | 0,6 dtk | 0,3 dtk |
| Best Practices | 96 | **100** | 100 | 100 |
| Accessibility | 91 | 91 | 88 | 88 |
| SEO | 85 | 85 | 85 | 85 |

Catatan: skor PageSpeed berfluktuasi ±10–30 poin antar tes (satu tes pukul 17:08 sempat 36). Untuk laporan dipakai tes 17:39.

---

## 5. Status Plugin Setelah Update

| Plugin | Versi Sekarang | Status |
|---|---|---|
| Backuply | 1.5.8 | ✅ Aman |
| Contact Form 7 | 6.1.7 | ✅ |
| Hello Plus | 1.7.8 | ✅ |
| Akismet | 5.7.2 | ✅ (nonaktif) |
| WP Mail SMTP | 4.9.0 | ✅ |
| WP Rocket | 3.23.3.3 | ✅ Aman |
| WPForms Lite | 2.0.2.1 | ✅ Aman |
| Converter for Media | terbaru | ✅ Baru dipasang |
| SeedProd | 6.18.18 | ⚠️ Vulnerable — update ke 6.20.9 tersedia, atau nonaktifkan kalau tidak dipakai |
| Elementor / Elementor Pro | 3.30.4 / 3.30.1 | ⚠️ Vulnerable — update ke 4.x gagal, ditahan untuk diuji di Staging |
| JetBlocks, JetElements, JetTricks, JetThemeCore | lama | ⚠️ Vulnerable — butuh **lisensi Crocoblock** untuk update |
| Crocoblock Wizard, SoftWP | — | Tidak perlu update |
| Tema GeneratePress | 3.6.0 | Update minor 3.6.1 tersedia (aman) |

Skor risiko keamanan WP Toolkit: **0,4 → 0,3**.

---

## 6. Temuan Penting untuk Disampaikan ke UOS

### Hasil audit backup (database + file, 28 Sep 2026)

1. **Link kontak mengarah ke data template (KRITIS).**

   | Lokasi | Teks yang tampil | Link sebenarnya |
   |---|---|---|
   | Footer #194 (semua halaman) | Email: office@uos.co.id | `mailto:contact@mysite.com` |
   | Footer #194 | WA: +62 818-0860-3153 | `tel:123-456-7890` |
   | Footer #194 | WA: +62 816-709-174 | `tel:123-456-7890` |
   | Footer #194 | Phone: +62 21-8428-3661 | `tel:123-456-7890` |
   | Kontak (widget icon-list `19c73afd`) | +62 818-0860-3153 | `tel:213-200-5078` |
   | Kontak | +62 816-709-174 | `tel:213-200-5078` |
   | Kontak | +62 21-8428-3661 | `tel:213-200-5078` |
   | Kontak | office@uos.co.id | `mailto:kevinclarkfit@training.com` |

   Hanya tombol WhatsApp di Beranda (`wa.me/6281808603153`) yang benar. Perbaikan: Elementor → edit Footer dan halaman Kontak → ganti link tiap item menjadi `https://wa.me/6281808603153`, `https://wa.me/62816709174`, `tel:+622184283661`, dan `mailto:office@uos.co.id`.
2. **Formulir Kontak (Elementor Pro, "Contact Us") belum pernah menghasilkan calon asli.** 102 kiriman: 3 tes developer (Jun 2025) dan 99 spam (penawaran jasa/backlink/AI berbahasa Inggris). Semua berstatus *belum dibaca*. Formulir juga **tanpa proteksi anti-spam** (reCAPTCHA/honeypot).
3. **Riwayat kegagalan email (log WP Mail SMTP):**
   - Jun 2025 – Mei 2026: notifikasi ke `admin@uos.co.id` gagal ratusan kali (*No such user*). **Email admin WordPress mengarah ke mailbox yang tidak ada.** Ganti di Settings → General → *Administration Email Address*, atau buat mailbox tersebut di cPanel.
   - Feb 2026 dan Jun – Sep 2026: *Could not connect to SMTP host*. Periode Juni–September cocok dengan SSL `mail.uos.co.id` yang kedaluwarsa, dan seharusnya pulih setelah SSL diperbarui (perlu dibuktikan dengan *Email Test*).
4. **Halaman publik yang seharusnya tidak tampil:** `uos.co.id/sample-page` (halaman bawaan WordPress) dan `uos.co.id/template` (berisi teks *Lorem ipsum*). Karena blokir Google sudah dibuka, keduanya bisa ikut terindeks. Ubah ke *Draft*.
5. **Dua akun Administrator:** `SuperAdmin` (domain uos.co.id, 20 Mei 2025) dan `admin` (Gmail, 20 Jul 2025). Konfirmasi ke UOS siapa pemilik akun `admin`. Kalau vendor lama, hapus atau turunkan hak aksesnya.
6. **Keamanan file:** tidak ada malware. File inti WordPress 6.7.9 (3.224 file) dan 9 plugin gratis identik dengan versi resmi wordpress.org. Plugin premium (Elementor Pro, Jet, WP Rocket, GP Premium) tidak mengandung pola kode berbahaya. Banyak file `error_log` di folder inti berasal dari bot yang mencoba mengakses file secara langsung (tidak berbahaya). Hardening yang disarankan: tambahkan `DISALLOW_FILE_EDIT` di wp-config.php, dan hapus duplikasi definisi `WP_DEBUG`.

### Temuan lain

7. **Website sempat tidak bisa ditemukan di Google** karena pengaturan *noindex*. Sudah dibuka hari ini.
8. **Lisensi Crocoblock** (JetElements, JetBlocks, JetTricks, JetThemeCore) perlu dikonfirmasi. Tanpa lisensi, celah keamanannya tidak bisa ditutup.
9. **Perpanjangan otomatis mati** untuk domain (5 Mei 2027), hosting (6 Mei 2027), dan SSL Sectigo (10 Jul 2027).
10. **Subdomain lama 2021** (cctv, hotspot, laporan, jadwal, cek, afiahkost) tercatat di riwayat SSL. Perlu dicek apakah masih aktif.

> Catatan privasi: backup diunduh sementara dari Google Drive SITUNEO untuk audit, lalu dihapus dari lingkungan analisis setelah selesai. Laporan ini hanya memuat angka agregat, tanpa data pribadi pengirim formulir.

---

## 7. Pekerjaan Tertunda (To-Do)

### Sisa scope Rp 1,5 jt
| # | Pekerjaan | Catatan |
|---|---|---|
| 1 | **Perbaiki link WA/telepon/email** di Footer #194 dan halaman Kontak | Prioritas tertinggi. Semua klik kontak saat ini hilang. |
| 2 | **Verifikasi email** (WP Mail SMTP → Tools → Email Test) dan ganti *Administration Email* dari `admin@uos.co.id` | Pastikan notifikasi formulir sampai |
| 2a | Tambahkan anti-spam pada formulir (Elementor → Settings → Integrations → reCAPTCHA v3, atau field *Honeypot*) | 99 dari 102 kiriman adalah spam |
| 2b | Ubah `sample-page` dan `template` ke Draft; konfirmasi akun admin `admin` | Kebersihan SEO dan keamanan |
| 3 | **Formulir di halaman depan** | Salin formulir Kontak ke Home01. Kolom: Nama, WhatsApp, Asal Sekolah, Program, Orang tua/Siswa, Persetujuan (UU PDP). Aktifkan *Collect Submissions*. |
| 4 | **Open Graph** (preview WhatsApp) | Pasang Yoast SEO, gambar 1200×630, SEO title dan meta description Beranda |
| 5 | **GA4 + Google Tag Manager** | Butuh akun Google milik UOS. Pixel Meta/TikTok menunggu akun iklan. |

### Perbaikan lanjutan (disarankan)
| # | Pekerjaan | Dampak |
|---|---|---|
| 6 | Hapus 322 komentar spam dan tutup fitur komentar | Kebersihan database, keamanan |
| 7 | Regenerate Thumbnails, lalu konversi ulang WebP | Sisa *image delivery* 617 KiB di mobile |
| 8 | Slider statis khusus HP (perlu persetujuan UOS) | LCP mobile di bawah ±4 detik |
| 9 | Update SeedProd dan tema GeneratePress 3.6.1 | Keamanan |
| 10 | Update Elementor 4.x dan WordPress 7.1.2 lewat **Staging** | Keamanan, kompatibilitas plugin baru |
| 11 | Perbaikan aksesibilitas: label ikon sosial, ukuran tombol di HP, urutan heading | Skor Accessibility/SEO naik ke 90+ |
| 12 | Cek *Site Health* (7 item, ada status *critical*) | Kesehatan situs |
| 13 | Minta klien ganti password Clientzone setelah proyek selesai | Keamanan akses |

---

## 8. Catatan Teknis (untuk rollback atau pemeliharaan)

- **SSL:** Let's Encrypt diterbitkan manual via cPanel → SSL/TLS Certificates → Wizard (Rumahweb, cPanel 138). Validasi HTTP-DCV lolos untuk semua domain. Perpanjangan otomatis perlu dipantau sekitar pertengahan Desember 2026.
- **PHP:** uos.co.id sekarang memakai **CloudLinux PHP Selector 8.1** (sebelumnya cPanel MultiPHP 8.1). Rollback: PHP Selector → Per Domain Settings → kembalikan ke MultiPHP Manager.
- **WP Rocket → File Optimization:** Minify CSS ✅, Optimize CSS delivery = Load CSS asynchronously ✅, Minify JS ✅, Combine JS ❌, Load JS deferred ✅, Delay JS ✅ (Safe Mode ✅). Kalau tampilan rusak, matikan berurutan: Delay JS → Optimize CSS delivery → Defer JS.
- **Converter for Media:** format WebP, strategi Optimal, folder /uploads, konversi otomatis untuk upload baru aktif, delivery via .htaccess.
- **Backup:** Softaculous menyimpan 2 backup (Jul 2025 dan 28 Sep 2026; batas 3). Salinan 28 Sep ada di komputer SITUNEO.
- **Firewall server:** permintaan berulang dari satu IP (±20+ request cepat) bisa diblokir sementara oleh firewall Rumahweb.

---

## 9. Koreksi untuk Proposal

- Hal. 3 menyebut sertifikat SSL "diterbitkan untuk nama yang salah (ipv6.uos.co.id)". Sertifikat lama memang memakai nama utama `ipv6.uos.co.id`, tetapi sudah mencakup `uos.co.id` dan `www`. **Masalah sebenarnya hanya kedaluwarsa.**

---

## 10. Peluang Lanjutan (Upsell)

| Layanan | Alasan |
|---|---|
| Paket maintenance bulanan | Update plugin tertunda, backup terakhir 419 hari, SSL sempat mati 4 bulan tanpa ada yang tahu |
| Staging dan update besar (Elementor 4, WP 7.1) | Plugin baru mulai tidak mendukung WP 6.7 |
| Kebijakan Privasi (Rp 150 rb) | Formulir baru mengumpulkan data siswa dan orang tua (UU PDP) |
| Artikel blog rutin | Artikel terakhir terbit Juni 2025 |
| Paket Menyeluruh (iklan, landing page, CRM) | Fondasi situs sekarang siap menerima trafik iklan |
