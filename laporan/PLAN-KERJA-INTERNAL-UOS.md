# Rencana Kerja Internal — Perbaikan Website UOS (Rp1.500.000)

> **INTERNAL SITUNEO. Jangan dikirim ke klien.** Untuk klien, pakai `Laporan-Perbaikan-Website-UOS-Tahap-1.pdf`.

**Klien:** PT Unggulan Operator Sinergis (UOS) · **Situs:** uos.co.id (WordPress + Elementor, hosting Rumahweb, cPanel)
**Paket:** Perbaikan & Optimasi Website — Rp1.500.000 (lunas)
**Target selesai:** ±5 hari kerja setelah akses dari UOS lengkap

---

## Ringkasan Progres

| # | Item paket | Status | Estimasi sisa |
|---|---|---|---|
| 1 | SSL & HTTPS | ✅ Selesai (28 Sep) | – |
| 2 | Kompres & WebP gambar | ✅ Selesai (65 file, hemat 44,75 MB) | – |
| 3 | Optimasi kecepatan (WP Rocket) | ✅ Selesai | – |
| 4 | Buka blokir Google (noindex) | ✅ Selesai | – |
| 5 | Update plugin aman (7 plugin) | ✅ Selesai | – |
| 6 | Konfigurasi server (PHP Selector 8.1 + gd/imagick/dom) | ✅ Selesai | – |
| 7 | Backup penuh + audit keamanan | ✅ Selesai | – |
| 8 | Perbaikan link WA/telepon/email (footer + Kontak) | ✅ Selesai (29 Sep, terverifikasi live) | – |
| 9 | Email notifikasi + test (SMTP OK, form Kontak → office@uos.co.id, Reply-To pengunjung, timezone Jakarta) | ✅ Selesai (29 Sep, email tes masuk Inbox) | – |
| 10 | Anti-spam formulir (Honeypot) + pesan formulir bahasa Indonesia | ✅ Selesai (29 Sep, terverifikasi live) | – |
| 11 | **Formulir di Beranda** | ⏳ Belum | 1–2 jam |
| 12 | **Tampilan link WhatsApp (Open Graph)** | ⏳ Belum | 1 jam |
| 13 | **GA4 + Google Tag Manager** | ⏳ Menunggu akses Google UOS | 1 jam |
| 14 | Meta & TikTok Pixel | ⏳ Menunggu akun iklan UOS | 30 menit |
| 15 | Bersihkan 322 komentar spam + tutup komentar & pingback | ✅ Selesai (29 Sep) | – |
| 16 | Nonaktifkan halaman contoh (sample-page, template → Draft, kini 404) | ✅ Selesai (29 Sep, terverifikasi live) | – |
| 17 | Uji akhir + PageSpeed akhir + laporan serah terima | ⏳ Belum | 1 jam |

**Total sisa kerja: ±1–1,5 hari kerja efektif.**

---

## Hari 1 — Menutup kebocoran calon (tanpa perlu akses tambahan)

### 8. Perbaiki link kontak ⚠️ PRIORITAS UTAMA
**A. Footer (tampil di semua halaman)**
1. WP Admin → **Templates → Theme Builder** → **Footer** (Elementor Footer #194) → **Edit with Elementor**
2. Klik widget daftar kontak (icon list), lalu klik tiap baris → bagian **Link**:
   | Teks | Link baru |
   |---|---|
   | Email: office@uos.co.id | `mailto:office@uos.co.id` |
   | WA: +62 818-0860-3153 | `https://wa.me/6281808603153` |
   | WA: +62 816-709-174 | `https://wa.me/62816709174` |
   | Phone: +62 21-8428-3661 | `tel:+622184283661` |
3. Kalau link memakai **ikon database (Dynamic Tag)**, klik ikon itu → **hapus dynamic tag** → isi link manual
4. **Update**

**B. Halaman Kontak** → Pages → Kontak → Edit with Elementor → ulangi langkah yang sama untuk widget kontak (3 nomor + email).

**C. Tes** di HP (Incognito): klik setiap link. WA harus membuka chat ke nomor UOS dan email harus membuka office@uos.co.id.
→ WP Rocket → **Clear cache**

### 9. Email notifikasi
1. **Settings → General → Administration Email Address** → ganti `admin@uos.co.id` menjadi `office@uos.co.id` (atau email yang dikonfirmasi UOS) → Save, lalu klik link konfirmasi yang dikirim ke email itu
2. **WP Mail SMTP → Tools → Email Test** → kirim ke email SITUNEO → harus *sent successfully* dan email benar-benar masuk (cek folder spam juga)
3. Kalau gagal: screenshot error-nya. Kemungkinan password SMTP `adminweb@uos.co.id` perlu dicek di cPanel → Email Accounts.
4. Formulir Kontak (Elementor) → **Actions After Submit → Email → To** = email aktif UOS

### 10. Anti-spam formulir
- Opsi cepat: Elementor Form → tambah field **Honeypot** (Pro) → Update
- Opsi kuat: **Elementor → Settings → Integrations → reCAPTCHA v3** (butuh site key dari akun Google; bisa pakai akun SITUNEO dulu) → tambah field reCAPTCHA v3 di form

### 15–16. Bersih-bersih
- **Comments → Pending** → Screen Options 999 → pilih semua → Move to Trash → Empty Trash
- **Settings → Discussion** → matikan *Allow people to submit comments on new posts*
- **Pages** → `Sample Page` dan `Template` → Quick Edit → Status **Draft**

---

## Hari 2 — Formulir Beranda & tampilan link WhatsApp

### 11. Formulir di Beranda
1. Pages → Kontak → Edit with Elementor → klik kanan form → **Copy** → keluar tanpa simpan
2. Pages → **Home01** → Edit with Elementor → section baru di bawah slider → **Paste**
3. Judul: **"Daftar Konsultasi Gratis"** · subjudul: *"Tim UOS akan menghubungi Anda lewat WhatsApp dalam 1×24 jam kerja."*
4. Kolom:
   | Kolom | Tipe | Wajib |
   |---|---|---|
   | Nama Lengkap | Text | ✅ |
   | Nomor WhatsApp | Tel | ✅ |
   | Asal Sekolah | Text | ✅ |
   | Program yang Diminati | Select: Kuliah D3 Plus di Tiongkok / Study Tour ke Tiongkok / Kursus Bahasa Mandarin / Belum tahu | ✅ |
   | Saya adalah | Radio: Orang tua / Siswa | – |
   | Persetujuan | Acceptance: "Saya setuju data ini digunakan UOS untuk menghubungi saya." | ✅ |
   | Honeypot / reCAPTCHA | – | – |
5. Actions After Submit: **Collect Submissions** ✅ + **Email** (To: email UOS, Subject: `Calon Baru dari Website – [field id="program"]`)
6. Success message: *"Terima kasih! Tim UOS akan segera menghubungi Anda lewat WhatsApp."*
7. Update → tes isi form dari HP → cek email masuk dan data di **Elementor → Submissions**

### 12. Tampilan link WhatsApp (Open Graph)
1. Plugins → Add New → **Yoast SEO** (cek *Compatible*) → Activate → lewati wizard atau isi sebagai Organization "PT Unggulan Operator Sinergis (UOS)"
2. Buat gambar 1200×630 di Canva (foto siswa + "Kuliah D3 & Magang Kerja di China" + logo), JPG < 300 KB → upload ke Media
3. Pages → Home01 → Edit (editor biasa) → kotak Yoast:
   - SEO title: `Kuliah D3 & Magang Kerja di China | UOS Education Consultant`
   - Meta description: `Kuliah vokasi 2 tahun + 1 tahun magang di perusahaan China, lalu penempatan kerja di Indonesia. Konsultasi gratis bersama UOS sejak 2011.`
   - Tab Social → gambar 1200×630
4. Yoast → Settings → Site basics → **Site image** = gambar yang sama
5. Clear cache WP Rocket → **developers.facebook.com/tools/debug** → Scrape Again → tes kirim link di WhatsApp

---

## Hari 3 — Tracking (setelah akses dari UOS)

### 13. GA4 + Google Tag Manager
1. Minta UOS: **email Google** yang akan jadi pemilik, lalu undang email SITUNEO sebagai **Editor/Admin**
2. Buat properti **GA4** (zona waktu Jakarta, mata uang IDR) → catat Measurement ID `G-XXXX`
3. Buat container **GTM** (Web) → catat `GTM-XXXX`
4. Pasang GTM: plugin **GTM4WP** atau Elementor → Custom Code (head + body)
5. Di GTM: tag **Google tag (GA4)** → trigger All Pages → Publish
6. Event konversi: **form submit** (formulir Beranda & Kontak) dan **klik WhatsApp** (link berisi `wa.me`) → tandai sebagai *Key event* di GA4
7. Tes dengan **Tag Assistant** + GA4 Realtime

### 14. Meta & TikTok Pixel
- Hanya kalau UOS sudah punya **Business Manager / TikTok Ads** (pembuatan akun iklan = layanan terpisah Rp1,5 jt)
- Pasang lewat GTM (template Meta Pixel / TikTok Pixel) + event *Lead* saat form submit

---

## Hari 4 — Uji akhir & serah terima

### 17. Checklist uji
- [ ] Semua halaman terbuka tanpa error (Beranda, Tentang Kami, Kompetensi, Berita, Kontak) di HP & laptop
- [ ] Semua link WA/telepon/email benar
- [ ] Formulir Beranda & Kontak: terkirim, email masuk, data tercatat di Submissions
- [ ] Preview WhatsApp muncul (gambar + judul)
- [ ] GA4 Realtime mencatat kunjungan & event form/WA
- [ ] `https://uos.co.id` gembok aman, `http://` & `www` teralihkan
- [ ] Tidak ada tag `noindex`
- [ ] PageSpeed akhir (Mobile & Desktop) → screenshot + *Copy Link*
- [ ] Backup akhir via Softaculous → simpan di Drive SITUNEO

### Serah terima
- Update PDF laporan (status ⏳ → ✅) → kirim ke UOS
- Minta UOS **ganti password Clientzone & cPanel** setelah pekerjaan selesai
- Tawarkan tahap lanjutan (lihat di bawah)

---

## Yang Harus Diminta dari UOS (kirim lewat sales, sekarang)

1. Email aktif penerima formulir (office@uos.co.id?)
2. Konfirmasi nomor WA: 0818-0860-3153 & 0816-709-174 masih aktif?
3. Akses akun Google untuk GA4/GTM
4. Status akun iklan (Meta/TikTok) → untuk pixel
5. Status lisensi Crocoblock
6. Pemilik akun admin `admin` (Gmail) → boleh dihapus?

---

## Di Luar Paket Rp1,5 jt → Tawarkan Terpisah (harga resmi situneo.my.id)

| Layanan | Biaya | Kapan ditawarkan |
|---|---|---|
| **Redesign — Paket Pendidikan (Website)** | Rp3.500.000 + Rp450.000/bln | Bersamaan dengan laporan tahap 1 |
| Update WordPress 7 & Elementor 4 via staging (Perbaikan Website Ringan) | Rp500.000 | Kalau UOS tidak ambil redesign |
| Kebijakan Privasi & S&K | Rp150.000 | Wajib sebelum formulir dipakai untuk iklan |
| Backup & Recovery | Rp100.000/bln | Kalau tidak ambil paket dengan pemeliharaan |
| Uji Menyeluruh Website | Rp750.000 | Sebelum kampanye iklan |
| Paket Menyeluruh (proposal) | Rp5,8 jt sisa sekali bayar + Rp3,1 jt/bln | Setelah tahap 2 selesai |
| CRM AI WhatsApp | Rp4,7 jt + Rp850 rb/bln | Bersama Paket Menyeluruh |

**Catatan batas scope:** jangan kerjakan redesign, landing page, atau update besar WordPress/Elementor dalam paket Rp1,5 jt. Kalau klien minta, arahkan ke penawaran terpisah.

---

## Catatan Teknis (rollback)

- **PHP:** uos.co.id memakai CloudLinux PHP Selector 8.1. Rollback: PHP Selector → Per Domain Settings → kembali ke MultiPHP Manager.
- **WP Rocket:** kalau tampilan rusak, matikan berurutan: Delay JS → Optimize CSS delivery → Defer JS.
- **Backup:** Softaculous → Backups (28 Sep 2026, 263 MB) + salinan di Drive SITUNEO.
- **Firewall Rumahweb:** permintaan beruntun dari satu IP bisa diblokir sementara. Jangan menguji situs secara berlebihan.
