# DATA STRUKTUR ENGAGEMENT LETTER — MENGIKUTI TEMPLATE QROCKETLAB

Gunakan struktur di bawah untuk mengisi template dokumen (cover → executive summary → snapshot → analisis per section → masalah/rekomendasi → priority matrix → footer), mengikuti pola dokumen referensi "Sunnyside Gaming BI Report".

---

## COVER PAGE

- **Label kategori:** ENGAGEMENT LETTER / PROJECT SCOPE DOCUMENT
- **Judul utama:** LAUNDRY CLUB
- **Subjudul:** AI Customer Service Assistant — Chatbot Implementation
- **Deskripsi singkat:** Website Chatbot untuk Laundry Club by CV Mahajaya Utama Bersama
- **Periode Analisis/Diskusi:** [tanggal discovery pertama] – Juli 2026
- **Tanggal Dokumen:** Juli 2026
- **Prepared by:** Abyan Hisyam Al'Ammar (Antonio) — QRocketLab
- **Klasifikasi:** CONFIDENTIAL

---

## SECTION 01 — Executive Summary

**Angka kunci (key metric boxes):**
- **3 Tier** — Roadmap scope bertahap yang ditawarkan (FAQ, Interactive, Lead Qualification)
- **Rp 80rb–260rb** — Estimasi biaya infra bulanan Tier 1 (scope awal disepakati)
- **11 Flow** — Proses CS eksisting client yang dipetakan sebagai basis knowledge & desain bot

**3 TEMUAN KRITIS**

| # | Temuan | Konteks Data | Implikasi |
|---|---|---|---|
| 01 | CS manual belum terskalakan | Seluruh proses CS (order, komplain, koordinasi) berjalan manual via WhatsApp + Telegram, terdokumentasi dalam 11 flow chart operasional client, dengan basis 250rb+ pelanggan di 17 kota | Volume pertanyaan repetitif berpotensi besar dan terus bertambah seiring pertumbuhan bisnis; risiko response time lambat & beban admin naik |
| 02 | Sebagian besar flow bersifat informasi, bukan aksi eksekusi | Dari 11 flow yang dipetakan, mayoritas tahap awal (deteksi lokasi, kirim pricelist, cek minat, kirim S&K) bersifat informasional dan dapat diotomasi; tahap eksekusi (booking driver, verifikasi pembayaran, investigasi komplain) tetap memerlukan aksi manusia atau integrasi API pihak ketiga | Chatbot dapat memberikan dampak signifikan pada porsi informasi tanpa perlu merombak keseluruhan proses transaksi yang sudah berjalan |
| 03 | Dependency pada API pihak ketiga menentukan batas otomasi | Booking driver terhubung ke Lalamove; Lalamove menyediakan API resmi (developers.lalamove.com) namun mensyaratkan pendaftaran partner terlebih dahulu | Tingkat otomasi Tier 2/3 (booking driver, cek ongkir otomatis) bersifat kondisional terhadap proses & approval partnership Lalamove yang berada di luar kendali vendor |

**TOP 3 REKOMENDASI**

1. **Mulai dari Tier 1 sebagai fase validasi**
   Implementasi FAQ & Info Assistant di website dengan pendekatan context stuffing (tanpa vector database) — biaya rendah, risiko rendah, dan hasil dapat divalidasi cepat sebelum melangkah ke tier lanjutan.

2. **Pertahankan WhatsApp sebagai satu-satunya jalur transaksi**
   Chatbot berfungsi sebagai layer penyaring & informasi di website; begitu pertanyaan mengarah pada transaksi atau di luar kapasitas bot, sistem otomatis mengarahkan (handoff) pengguna ke WhatsApp yang sudah menjadi channel utama operasional.

3. **Ajukan pendaftaran partner Lalamove API sejak awal**
   Mengingat proses approval partnership berada di luar kendali vendor dan berpotensi memakan waktu, pengajuan sebaiknya dimulai paralel dengan pengerjaan Tier 1 agar tidak menjadi bottleneck saat proyek memasuki Tier 3.

**PELUANG BISNIS TERIDENTIFIKASI**

| Peluang | Nilai | Deskripsi |
|---|---|---|
| Efisiensi Biaya Infra | Rp 80rb–260rb/bln | Estimasi biaya operasional Tier 1 dengan pendekatan context stuffing + hosting SemutSSH Cloud, jauh lebih rendah dibanding pendekatan vector DB konvensional |
| Deflection Rate CS | TBD saat discovery | Potensi pengurangan volume pertanyaan repetitif yang masuk ke admin manual, meningkatkan efisiensi waktu tim CS |
| Kualitas Lead Franchise | Tiket Rp 65jt+/lead | Tier 3 berpotensi meningkatkan kualitas lead franchise melalui kualifikasi otomatis sebelum diteruskan ke tim sales |

---

## SECTION 02 — Project Snapshot

| KPI | Nilai | Keterangan |
|---|---|---|
| Jumlah Tier Roadmap | 3 Tier | Basic (FAQ), Medium (Interactive), Advanced (Lead Qualification) |
| Channel Chatbot | Website only | Widget chat, bukan integrasi WhatsApp Business API |
| Channel Transaksi | WhatsApp (tetap) | Tidak berubah dari proses eksisting |
| Flow Operasional Dipetakan | 11 flow | Sumber: dokumen "Flow Kerja CS" milik client (order masuk, member, driver sendiri, repeat, promo, komplain x5) |
| Pendekatan Knowledge Base | Context stuffing | Tanpa vector database — sesuai skala konten client saat ini |
| Estimasi Biaya Tier 1 | Rp 80rb–260rb/bln | Hosting + LLM API, di luar fee development |
| Estimasi Biaya Tier 2 | Rp 350rb–750rb/bln | Bergantung pada ketersediaan API sistem status cucian internal client |
| Estimasi Biaya Tier 3 | Rp 720rb–1,7jt/bln | Bergantung pada partnership Lalamove API & integrasi CRM |

---

## SECTION 03 — Ruang Lingkup & Arsitektur per Tier

### TIER 1 — FAQ & Info Assistant (Scope Disepakati untuk Dieksekusi)

| Komponen | Detail |
|---|---|
| Channel | Widget chat website |
| Kemampuan | Jawab harga, jam operasional, area coverage, cara kerja layanan, S&K, info promo; jelaskan benefit member (informasional); intake form order; intake komplain terstruktur |
| Referensi Flow Client | Chat Customer Masuk Umum, Chat Jika Member, Promo Laundry Time/Senin Fresh Deal |
| Batasan | Tidak memproses transaksi/pembayaran; tidak memutuskan hasil investigasi komplain atau ganti rugi |
| Strategi Handoff | Intent-based (niat transaksi/komplain terdeteksi → tombol ke WA) + Fallback-based (di luar cakupan pengetahuan → arahkan ke WA) |
| Arsitektur | n8n (orchestration) + LLM API murah (DeepSeek/Groq atau setara) + context stuffing (tanpa vector DB) |
| Hosting | SemutSSH Cloud, paket Worker (1024MB RAM, 1 Core, 10GB Storage) |
| Estimasi Biaya | Rp 80.000–260.000/bulan |

### TIER 2 — Interactive Assistant (Tahap Lanjutan)

| Komponen | Detail |
|---|---|
| Kemampuan Tambahan | Cek status cucian real-time, rekomendasi layanan personal |
| Dependency | API sistem status cucian internal client (`apps.laundryclub.co.id`) — ketersediaan perlu dikonfirmasi |
| Prasyarat Eksekusi | Validasi hasil Tier 1 selesai |
| Estimasi Biaya | Rp 350.000–750.000/bulan |

### TIER 3 — Lead Qualification & Business Assistant (Tahap Lanjutan)

| Komponen | Detail |
|---|---|
| Kemampuan Tambahan | Pemisahan jalur customer vs franchise; kualifikasi lead franchise otomatis (modal, kota, timeline); data terstruktur ke CRM/sheet tim sales; potensi booking driver otomatis |
| Dependency Kritis | Lalamove Partner API (developers.lalamove.com) — memerlukan pendaftaran partner resmi; approval di luar kendali vendor |
| Ketentuan Audit Trail | Notifikasi ke Telegram tim crew/operasional dipertahankan sepenuhnya sebagai jalur dokumentasi internal (form order, struk, timbangan, bukti pembayaran, link tracking) — konsisten dengan pola yang berlaku di seluruh 11 flow operasional client, bukan digantikan oleh bot |
| Estimasi Biaya | Rp 720.000–1.700.000/bulan |

---

## SECTION 04 — Pemetaan Flow Operasional Client (Referensi Teknis)

| Flow Client | Kategori | Realistis Diotomasi di Tier 1? |
|---|---|---|
| Chat Customer Masuk Umum | Informasi + Order Intake | Ya (bagian informasi & form) |
| Chat Jika Member | Informasi + Approval | Sebagian — approval top-up tetap manual |
| Chat Member Non-Free-Ongkir | Informasi | Ya |
| Chat Pesan Driver Sendiri | Informasi | Ya (bagian pricelist & konfirmasi) |
| Chat Repeat Order | Informasi + Booking | Sebagian — booking driver tetap manual hingga Tier 3 |
| Promo Laundry Time/Senin Fresh Deal | Informasi | Ya |
| Chat Customer Tidak Jadi Cuci | Informasi | Ya |
| Komplain Kehilangan | Investigasi | Intake saja — keputusan tetap manusia |
| Komplain Cucian Luntur | Investigasi + Keputusan Pola | Intake + penawaran awal — eksekusi tetap manusia |
| Komplain Pakaian Rusak | Investigasi | Intake saja — keputusan tetap manusia |
| Komplain Tidak Sesuai/Sesuai SNK | Investigasi + Tracking | Intake saja — tracking tetap Admin Operasional |

---

## SECTION 05 — Masalah/Dependency Terdeteksi & Rekomendasi

**DEPENDENCY TINGKAT TINGGI**

| ID | Dependency | Detail | Rekomendasi |
|---|---|---|---|
| DEP-001 | Lalamove Partner API | Booking driver otomatis (Tier 3) memerlukan status partner resmi Lalamove; proses approval di luar kendali vendor | Ajukan pendaftaran partner paralel dengan pengerjaan Tier 1 agar tidak menjadi bottleneck di Tier 3 |
| DEP-002 | API Sistem Status Cucian | Fitur cek status real-time (Tier 2) memerlukan akses API dari sistem internal client (`apps.laundryclub.co.id`) | Konfirmasi ketersediaan & dokumentasi API ke tim internal/vendor sistem client sebelum Tier 2 dimulai |
| DEP-003 | Sistem Member/Top-up | Client sudah memiliki aplikasi untuk top-up member (bukan proses manual/spreadsheet), namun approval top-up tetap dilakukan manual melalui grup koordinasi internal | Konfirmasi apakah aplikasi top-up member memiliki API yang dapat diintegrasikan; approval tetap menjadi proses manusia pada semua tier terlepas dari hasil konfirmasi API |
| DEP-004 | Kewenangan Bot atas Keputusan Berbasis SOP Sederhana | Sebagian kasus komplain (mis. cucian luntur kategori satuan) mengikuti SOP yang cukup sederhana dan berpotensi ditawarkan otomatis oleh bot (mis. penawaran rewash), namun kewenangan bot untuk mengambil keputusan meski kecil perlu disepakati eksplisit dengan client | Tier 1 diposisikan sebagai intake terstruktur untuk seluruh kasus komplain; opsi bot menawarkan solusi awal berbasis SOP sederhana (tanpa keputusan final) dapat dieksplorasi sebagai pengembangan lanjutan setelah kesepakatan eksplisit dengan client |

**PELUANG TERIDENTIFIKASI**

| ID | Temuan | Nilai Bisnis | Rekomendasi |
|---|---|---|---|
| OPP-001 | Biaya infra Tier 1 sangat rendah | Rp 80rb–260rb/bulan | Jadikan Tier 1 sebagai low-risk quick win untuk membangun kepercayaan sebelum upsell ke tier lanjutan |
| OPP-002 | Mayoritas flow bersifat informasional | 7 dari 11 flow dominan informasi | Fokuskan Tier 1 pada flow-flow ini untuk dampak maksimal dengan effort minimal |
| OPP-003 | Lead franchise bernilai tinggi | Tiket Rp 65jt+/lead | Tier 3 berpotensi memberikan ROI tertinggi relatif terhadap biaya infra bulanan |

---

## SECTION 06 — Priority Matrix (Roadmap Eksekusi)

| Prioritas | Inisiatif | Dampak | Effort | Timeline Indikatif |
|---|---|---|---|---|
| P1 | Implementasi Tier 1 — FAQ & Info Assistant | Mengurangi beban pertanyaan repetitif, respons 24/7 | Rendah–Sedang | [isi sesuai kesepakatan meeting] |
| P1 | Pengajuan Partnership Lalamove API | Membuka jalur otomasi booking driver di Tier 3 | Rendah (administratif) | Mulai paralel dengan Tier 1 |
| P2 | Konfirmasi ketersediaan API status cucian | Menentukan kelayakan Tier 2 | Rendah (discovery) | Setelah Tier 1 live |
| P2 | Implementasi Tier 2 — Interactive Assistant | Mengurangi friksi channel (web-WA-app terpisah) | Sedang | Setelah Tier 1 tervalidasi |
| P3 | Implementasi Tier 3 — Lead Qualification | Peningkatan kualitas lead franchise | Sedang–Tinggi | Setelah Tier 2 tervalidasi & Lalamove partnership approved |

---

## SECTION 07 — Ketentuan Umum untuk Engagement Letter

**Di Luar Ruang Lingkup (Out of Scope):**
- Integrasi WhatsApp Business API (channel transaksi tetap manual seperti saat ini)
- Keputusan otomatis atas kasus komplain (ganti rugi, hasil investigasi) — tetap wewenang tim client
- Booking driver otomatis & integrasi member otomatis, kecuali dependency terkait telah tersedia dan disepakati dalam adendum terpisah

**Asumsi:**
- Client menyediakan akses/konten knowledge base terkini (harga, S&K, FAQ) untuk Tier 1
- Verifikasi ketersediaan API (status cucian, member) menjadi tanggung jawab bersama saat proses discovery lanjutan
- Estimasi biaya bersifat indikatif, dapat berubah menyesuaikan harga API/hosting aktual dan volume riil penggunaan

**Item administratif yang perlu diisi setelah kesepakatan final:**
- [ ] Skema fee development & retainer maintenance bulanan
- [ ] Milestone pembayaran
- [ ] Tanggal mulai proyek & target go-live Tier 1
- [ ] PIC dari sisi client
- [ ] Konfirmasi ketersediaan API aplikasi top-up member (DEP-003) dan sistem status cucian (DEP-002)

---

## FOOTER / DISCLAIMER (mengikuti gaya template)

*Dokumen ini disusun berdasarkan hasil diskusi discovery dan data yang tersedia dari klien per Juli 2026. QRocketLab tidak bertanggung jawab atas keputusan bisnis yang diambil di luar konteks dokumen ini. Untuk pertanyaan, pembaruan scope, atau layanan lanjutan, hubungi tim QRocketLab.*

**Contact:** [isi email/kontak QRocketLab kamu]
