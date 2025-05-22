**Product Requirements Document (PRD)**

## Project Title

**iPusnas+ : Digital Social Library Platform**

---

## 1. Executive Summary

Aplikasi ini merupakan versi modern dan lebih lengkap dari iPusnas, yang berfungsi sebagai perpustakaan digital sosial berbasis web dan mobile. Pengguna dapat membaca, meminjam, mengunduh buku digital, dan berinteraksi dengan pengguna lain melalui ulasan, diskusi, dan fitur jejaring sosial. Admin dapat mengelola konten, statistik, dan aktivitas pengguna dengan dashboard lengkap.

---

## 2. Goals and Objectives

* Memberikan akses gratis ke ribuan buku digital.
* Menyediakan pengalaman sosial membaca buku seperti "Goodreads + Perpustakaan Digital".
* Memungkinkan peminjaman buku digital dengan waktu terbatas.
* Mengembangkan sistem rekomendasi berbasis minat dan aktivitas pengguna.

---

## 3. Target Users

* Pelajar dan Mahasiswa
* Pustakawan dan Guru
* Masyarakat Umum (semua umur)
* Admin Perpustakaan / Dinas Pendidikan

---

## 4. Core Features

### 4.1. User Authentication

* Email/password, OTP via SMS, dan Google OAuth (menggunakan Supabase Auth)
* Lupa password, verifikasi email

### 4.2. User Profiles

* Biodata, avatar, minat membaca, status (aktif/nonaktif)
* Lencana pencapaian (achievement)

### 4.3. Book Catalog

* List buku digital berdasarkan kategori dan genre
* Pencarian berdasarkan judul, penulis, ISBN, penerbit, kata kunci
* Filter: kategori, format, tahun, penilaian, popularitas

### 4.4. Book Detail

* Sampul, ringkasan, detail metadata (ISBN, tahun, bahasa, penerbit)
* Jumlah total eksemplar digital, sisa kuota peminjaman

### 4.5. Book Borrowing System

* Peminjaman dengan masa berlaku (1-7 hari)
* Sistem antre jika buku habis kuota
* Peringatan pengembalian otomatis
* Pembatasan jumlah peminjaman aktif

### 4.6. Reading System

* EPUB/PDF Reader dengan mode malam, font, bookmark, dan penanda halaman
* Reading progress (dalam persen dan waktu)
* Unduh untuk baca offline (dengan DRM)

### 4.7. Social Features

* Rating dan review (moderasi admin)
* Forum diskusi buku
* Ikuti pengguna lain dan lihat aktivitas mereka
* Berbagi ke media sosial

### 4.8. Personal Library

* Buku favorit
* Buku yang sedang dibaca / riwayat
* Wishlist / ingin dibaca

### 4.9. Notifications

* Push notifications untuk pengembalian, rekomendasi, status peminjaman, dll

### 4.10. Admin Dashboard

* CRUD Buku, Pengguna, Kategori
* Statistik peminjaman, buku populer, pengguna aktif
* Moderasi ulasan dan laporan penyalahgunaan

### 4.11. Recommendation Engine

* Berdasarkan minat, kategori populer, aktivitas sebelumnya

---

## 5. Non-Functional Requirements

* Responsif: UI berfungsi di mobile, tablet, dan desktop
* Skalabilitas: dapat menampung ribuan pengguna bersamaan
* Keamanan: Autentikasi JWT (Supabase), hashing password, sanitasi input
* Kinerja: waktu respon < 1 detik untuk permintaan umum
* Ketersediaan: 99.5% uptime SLA

---

## 6. Tech Stack

* **Frontend Web**: React.js, Tailwind CSS
* **Mobile**: React Native / Flutter
* **Backend**: Supabase (PostgreSQL + Supabase Auth + Supabase Storage + Realtime)
* **Database**: Supabase (PostgreSQL)
* **Auth**: Supabase Auth (Email, Magic Link, OAuth)
* **File Storage**: Supabase Storage
* **Realtime**: Supabase Realtime (untuk diskusi dan aktivitas sosial)
* **Monitoring**: Sentry, Grafana

---

## 7. Database (ERD - Singkat)

### Tables:

* Users (id, name, email, role, bio, avatar, preferences)
* Books (id, title, author, ISBN, publisher, category\_id, format, total\_copies, cover\_url, file\_url)
* Borrowings (id, user\_id, book\_id, borrowed\_at, due\_date, returned\_at)
* Categories (id, name)
* Reviews (id, user\_id, book\_id, rating, comment, created\_at)
* Favorites (id, user\_id, book\_id)
* Notifications (id, user\_id, message, is\_read, created\_at)
* Discussions (id, book\_id, user\_id, message, created\_at)
* Followers (id, user\_id, target\_user\_id)
* Admins (id, user\_id, permissions)

---

## 8. User Journey

1. **Registrasi dan Login (Supabase Auth)**
2. **Pilih minat kategori buku**
3. **Jelajah katalog dan pinjam buku**
4. **Baca buku via EPUB/PDF reader**
5. **Berinteraksi: ulas, beri rating, diskusi**
6. **Cek rak buku pribadi dan statistik baca**
7. **Admin mengelola konten dan pengguna melalui Supabase Dashboard atau panel kustom**

---

## 9. Success Metrics

* > 10.000 pengguna aktif dalam 6 bulan
* Rata-rata rating pengguna > 4.2
* Waktu baca pengguna rata-rata > 20 menit/hari
* < 1% crash/error rate

---

## 10. Roadmap Perkembangan

### Fase 1 (Minggu 1-2):

* Desain UI/UX
* Setup Supabase project dan database schema
* Autentikasi pengguna dan penyimpanan file (ebook)

### Fase 2 (Minggu 3-4):

* Katalog buku dan peminjaman (Supabase table + row-level security)
* EPUB/PDF reader terintegrasi

### Fase 3 (Minggu 5-6):

* Fitur sosial (review, diskusi, followers)
* Admin dashboard (manual via Supabase UI atau frontend khusus)

### Fase 4 (Minggu 7-8):

* Rekomendasi pintar (berbasis SQL view + API Supabase)
* Notifikasi dan deployment
* QA akhir dan peluncuran
