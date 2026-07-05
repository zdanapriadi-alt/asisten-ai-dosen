# Buku Panduan Pengguna — QuantumBot

**Sistem Chatbot Asisten Microcontroller**
Mata Kuliah Mikroprosessor — Fakultas Teknik, Universitas Negeri Yogyakarta

---

**Versi Dokumen:** 1.0
**Tanggal:** April 2026
**Diperuntukkan bagi:** Dosen dan Mahasiswa pengguna platform QuantumBot

---

## Daftar Isi

1. Pengenalan Antarmuka Utama
2. Cara Akses dan Login
3. Prosedur Pengoperasian — Antarmuka Chat (Mahasiswa)
4. Prosedur Pengoperasian — Panel Admin (Dosen)
5. Indikator Visual dan Notifikasi
6. Troubleshooting Pengguna

---

# BAB 1 — Pengenalan Antarmuka Utama

## 1.1 Tentang QuantumBot

QuantumBot adalah platform chatbot asisten berbasis web yang dikembangkan secara khusus untuk mendukung proses pembelajaran Mata Kuliah Mikroprosessor di Fakultas Teknik, Universitas Negeri Yogyakarta. Sistem ini lahir dari kebutuhan nyata di lapangan: mahasiswa seringkali membutuhkan jawaban cepat atas pertanyaan teknis seputar pemrograman microcontroller di luar jam perkuliahan, sementara dosen tidak selalu dapat hadir setiap saat. QuantumBot hadir sebagai jembatan antara keduanya — sebuah asisten digital yang tersedia sepanjang waktu, terfokus pada topik yang relevan, dan sepenuhnya berada di bawah kendali dosen.

Secara teknis, QuantumBot dibangun di atas teknologi kecerdasan buatan (AI) generatif yang kompatibel dengan antarmuka OpenAI. Model AI yang digunakan dapat dikonfigurasi oleh dosen sesuai kebutuhan, mulai dari model standar hingga model yang lebih canggih (Pro Model). Seluruh sistem berjalan di atas server Node.js dengan framework Express, yang menjamin kecepatan respons dan kemudahan pengelolaan di lingkungan lokal maupun server kampus.

Nama "QuantumBot" dipilih untuk mencerminkan presisi dan kecepatan komputasi — dua nilai inti yang juga menjadi fondasi ilmu microcontroller itu sendiri. Layaknya sebuah kuantum yang bergerak dalam dua keadaan sekaligus, QuantumBot melayani dua peran secara bersamaan: sebagai mitra belajar bagi mahasiswa, dan sebagai alat bantu pengajaran bagi dosen.

**Cakupan Topik yang Didukung**

QuantumBot dirancang sebagai asisten yang terfokus (domain-restricted), artinya sistem ini secara eksplisit membatasi diri hanya pada topik-topik yang relevan dengan mata kuliah. Topik-topik yang didukung meliputi pemrograman mikrokontroler Arduino (Uno, Mega, Nano, dan variannya), platform IoT berbasis ESP32 dan ESP8266 termasuk koneksi WiFi dan Bluetooth, mikrokontroler STM32 untuk aplikasi industri dan embedded system, Raspberry Pi untuk proyek single-board computer, serta berbagai jenis sensor dan aktuator elektronika seperti sensor suhu DHT22, sensor jarak ultrasonik HC-SR04, motor servo, relay, dan sebagainya. Selain itu, QuantumBot mampu menampilkan diagram pinout komponen secara visual langsung di dalam percakapan, sehingga mahasiswa tidak perlu beralih ke sumber lain untuk mendapatkan referensi teknis.

Pertanyaan yang berada di luar cakupan topik tersebut akan ditolak secara otomatis oleh sistem dengan respons yang sopan dan informatif. Kebijakan ini dapat diubah oleh dosen melalui Panel Admin jika diperlukan fleksibilitas topik yang lebih luas.

**Arsitektur Sistem dan Keamanan**

Dari sisi arsitektur, QuantumBot terdiri dari tiga komponen utama yang bekerja secara terpadu. Pertama adalah antarmuka frontend yang diakses melalui browser — terdiri dari tiga halaman utama yaitu halaman Login, halaman Chat untuk mahasiswa, dan halaman Admin Panel untuk dosen. Ketiga halaman ini dibangun dengan teknologi web standar (HTML, CSS, JavaScript) sehingga dapat diakses dari perangkat apa pun tanpa perlu instalasi aplikasi tambahan.

Komponen kedua adalah server backend berbasis Node.js dan Express yang menangani seluruh logika bisnis: autentikasi pengguna, manajemen sesi, routing antarmuka, pencatatan log aktivitas, serta komunikasi dengan layanan AI eksternal. Komponen ketiga adalah basis data berbasis file JSON yang menyimpan data pengguna, kelas, konfigurasi sistem, dan riwayat aktivitas secara persisten di sisi server.

Dari sisi keamanan, QuantumBot menerapkan sejumlah mekanisme perlindungan yang penting untuk lingkungan akademik. Sistem menerapkan kebijakan satu akun satu perangkat (single-device session), yang berarti satu akun tidak dapat digunakan secara bersamaan dari dua browser atau perangkat yang berbeda. Sesi pengguna akan berakhir secara otomatis setelah dua jam tidak aktif untuk mencegah penyalahgunaan akses. Sistem juga memiliki pembatas laju login (rate limiter) yang akan mengunci percobaan login setelah sepuluh kali gagal dalam rentang 15 menit, sebagai perlindungan terhadap serangan brute-force. Password pengguna disimpan dalam format hash bcrypt yang tidak dapat dibaca secara langsung, sehingga keamanan data tetap terjaga meskipun file database diakses oleh pihak yang tidak berwenang.

**Peran QuantumBot dalam Proses Pembelajaran**

QuantumBot tidak dirancang untuk menggantikan peran dosen, melainkan untuk memperkuat dan memperluas jangkauan proses pembelajaran. Dengan QuantumBot, mahasiswa dapat mengajukan pertanyaan teknis kapan saja — baik saat mengerjakan tugas di malam hari, saat praktikum di laboratorium, maupun saat menghadapi kendala di tengah persiapan ujian. Dosen, di sisi lain, tetap memegang kendali penuh atas konten yang diajarkan: mereka dapat mengunggah materi perkuliahan dalam format PDF, yang kemudian akan digunakan oleh QuantumBot sebagai referensi tambahan saat menjawab pertanyaan mahasiswa. Dengan cara ini, jawaban yang diberikan QuantumBot tidak hanya bersumber dari pengetahuan model AI umum, tetapi juga disesuaikan dengan materi dan konteks spesifik yang telah diajarkan oleh dosen di kelas.

Fitur pemantauan live status memungkinkan dosen melihat siapa saja mahasiswa yang sedang aktif menggunakan sistem secara real-time. Fitur log aktivitas memungkinkan dosen meninjau seluruh pertanyaan yang pernah diajukan beserta waktunya, sehingga dosen dapat memahami topik mana yang paling banyak menimbulkan kebingungan dan menyesuaikan materi pengajaran di pertemuan berikutnya. Kombinasi fitur-fitur ini menjadikan QuantumBot bukan sekadar chatbot, melainkan sebuah ekosistem pembelajaran digital yang terintegrasi dan terkelola dengan baik.

## 1.2 Dua Peran Pengguna

Sistem QuantumBot membedakan dua jenis pengguna dengan hak akses yang berbeda.

**Mahasiswa** mendapatkan akses ke halaman chat dan dapat mengajukan pertanyaan seputar microcontroller. Mahasiswa tidak dapat mengakses konfigurasi sistem maupun data pengguna lain.

**Dosen** mendapatkan akses ke Panel Admin yang lengkap, mencakup pengaturan bot, manajemen kelas dan akun mahasiswa, pemantauan aktivitas, dan kontrol sesi pembelajaran.

## 1.3 Tiga Halaman Utama

Sistem terdiri dari tiga halaman utama yang dapat diakses melalui browser.

**Halaman Login** adalah pintu masuk untuk semua pengguna. Semua pengguna diarahkan ke halaman ini terlebih dahulu sebelum dapat mengakses sistem.

**Halaman Chat** adalah antarmuka percakapan untuk mahasiswa. Setelah login berhasil, mahasiswa langsung diarahkan ke halaman ini.

**Panel Admin** adalah dasbor manajemen untuk dosen. Setelah login berhasil, dosen langsung diarahkan ke halaman ini.

[MASUKKAN GAMBAR: Diagram alur navigasi tiga halaman utama — Login → Chat (Mahasiswa) / Panel Admin (Dosen), dengan panah menunjukkan arah redirect berdasarkan peran]

---

# BAB 2 — Cara Akses dan Login

## 2.1 Persyaratan Akses

Sebelum menggunakan QuantumBot, pastikan hal-hal berikut terpenuhi. Pengguna membutuhkan perangkat (komputer, laptop, atau tablet) dengan browser modern seperti Google Chrome, Mozilla Firefox, atau Microsoft Edge versi terkini. Perangkat harus terhubung ke jaringan yang sama dengan server QuantumBot (misalnya jaringan lokal laboratorium atau internet jika server dipublikasikan). Pengguna harus sudah memiliki akun yang dibuat oleh dosen.

## 2.2 Mengakses URL Sistem

Buka browser dan ketikkan alamat URL server QuantumBot pada bilah alamat (address bar), contohnya:

**http://[alamat-server]:3000**

Gantilah [alamat-server] dengan alamat IP atau nama domain yang diberikan oleh dosen atau teknisi. Jika sistem berjalan di komputer yang sama (lokal), gunakan:

**http://localhost:3000**

Setelah menekan Enter, browser akan otomatis mengarahkan Anda ke **Halaman Login**.

[MASUKKAN GAMBAR: Tampilan browser menuju URL QuantumBot, menunjukkan address bar dengan URL diketik dan halaman login yang muncul]

## 2.3 Prosedur Login

[MASUKKAN GAMBAR: Halaman Login QuantumBot — tampilan kartu gelap di tengah layar dengan logo QuantumBot di bagian atas, kolom Username, kolom Password, dan tombol Masuk berwarna biru]

Ikuti langkah-langkah berikut untuk masuk ke sistem.

**Langkah 1:** Pada kolom **Username**, ketikkan username Anda yang telah diberikan oleh dosen.

**Langkah 2:** Pada kolom **Password**, ketikkan password Anda.

**Langkah 3:** Klik tombol **Masuk** berwarna biru. Sistem akan memproses permintaan login — tombol akan menampilkan animasi loading selama proses berlangsung.

**Langkah 4:** Jika berhasil, Anda akan diarahkan secara otomatis ke halaman yang sesuai dengan peran Anda. Mahasiswa akan masuk ke Halaman Chat, sedangkan Dosen akan masuk ke Panel Admin.

## 2.4 Pesan Kesalahan Saat Login

Jika login gagal, sebuah kotak pesan berwarna merah akan muncul di bawah tombol **Masuk** dengan keterangan penyebab kegagalan. Berikut pesan yang mungkin muncul dan artinya.

| Pesan Error | Artinya |
|---|---|
| Username atau password salah | Kredensial yang dimasukkan tidak sesuai. Periksa kembali. |
| Akun sedang digunakan di perangkat lain! | Akun Anda sedang aktif di browser/perangkat lain. Lakukan logout terlebih dahulu. |
| Akses kelas ini sedang ditutup oleh Dosen. | Dosen telah menonaktifkan akses kelas Anda sementara. |
| Terlalu banyak percobaan login. Coba lagi dalam 15 menit. | Sistem mengunci sementara karena terlalu banyak percobaan gagal. |
| Tidak dapat terhubung ke server. Periksa koneksi Anda. | Server tidak dapat dijangkau. Periksa koneksi jaringan. |

[MASUKKAN GAMBAR: Contoh tampilan kotak pesan error berwarna merah di bawah tombol Masuk, menampilkan salah satu pesan kesalahan di atas]

## 2.5 Keamanan Sesi

Sistem QuantumBot menerapkan mekanisme **sesi tunggal perangkat** — satu akun hanya dapat digunakan pada satu browser/perangkat pada satu waktu. Sesi akan berakhir otomatis setelah **2 jam** tidak aktif. Saat tab atau browser ditutup, sistem mendeteksi hal tersebut dan sesi dihentikan secara otomatis.

---

# BAB 3 — Prosedur Pengoperasian: Antarmuka Chat (Mahasiswa)

## 3.1 Mengenal Antarmuka Chat

[MASUKKAN GAMBAR: Tampilan lengkap Halaman Chat QuantumBot — bagian header atas dengan logo dan nama, area welcome screen di tengah dengan ikon logo besar dan chip saran pertanyaan, serta area input di bawah]

Halaman Chat terdiri dari tiga bagian utama.

**Header (Bagian Atas)** menampilkan logo dan nama QuantumBot di sisi kiri, badge nama model AI yang digunakan di tengah, indikator status berupa titik hijau berkedip yang menandakan sistem aktif, dan tombol **Logout** di sisi kanan.

**Area Percakapan (Bagian Tengah)** adalah tempat pesan Anda dan balasan QuantumBot ditampilkan. Saat pertama kali masuk, area ini menampilkan **Welcome Screen** dengan salam, deskripsi singkat, dan beberapa **Chip Saran Pertanyaan**.

**Input Bar (Bagian Bawah)** adalah tempat Anda mengetik pertanyaan dan mengirimkannya.

## 3.2 Mengajukan Pertanyaan

**Langkah 1:** Klik pada kolom input di bagian bawah layar yang bertuliskan placeholder teks.

**Langkah 2:** Ketikkan pertanyaan Anda seputar microcontroller atau elektronika. Contoh: *"Bagaimana cara membuat LED berkedip dengan Arduino?"*

**Langkah 3:** Tekan tombol **Kirim** (ikon panah) atau tekan tombol **Enter** pada keyboard untuk mengirim pesan.

**Langkah 4:** Tunggu beberapa saat. QuantumBot akan menampilkan animasi indikator sedang mengetik, kemudian jawaban akan muncul secara otomatis di area percakapan.

[MASUKKAN GAMBAR: Area percakapan yang menampilkan bubble pesan pengguna di sisi kanan (berwarna lebih terang) dan bubble balasan QuantumBot di sisi kiri dengan avatar bot, beserta animasi loading/typing indicator]

## 3.3 Menggunakan Chip Saran Pertanyaan

Saat Welcome Screen ditampilkan (sebelum ada percakapan), terdapat beberapa **Chip Saran** berupa tombol oval kecil yang berisi contoh pertanyaan populer. Klik salah satu chip untuk langsung mengirim pertanyaan tersebut tanpa perlu mengetiknya secara manual.

[MASUKKAN GAMBAR: Tampilan Welcome Screen dengan empat chip saran pertanyaan berbentuk oval, misalnya: "Cara blink LED dengan Arduino", "Tampilkan pinout Arduino Uno", "Cara koneksi ESP32 ke WiFi", "Cara pakai sensor DHT22 dengan Arduino"]

## 3.4 Memulai Percakapan Baru

Riwayat percakapan tidak tersimpan secara permanen — percakapan bersifat sementara dan akan terhapus saat halaman di-refresh atau Anda logout. Untuk memulai percakapan baru dari awal, cukup **refresh halaman** browser Anda (tekan F5 atau Ctrl+R).

## 3.5 Topik yang Dapat Ditanyakan

QuantumBot dirancang khusus untuk topik-topik berikut. Pertanyaan di luar topik ini akan ditolak dengan sopan oleh sistem.

- Pemrograman Arduino (sketch, fungsi, library)
- Microcontroller ESP32 dan ESP8266 (WiFi, Bluetooth, sensor)
- Microcontroller STM32 dan Raspberry Pi
- Rangkaian sensor dan aktuator elektronika
- Pinout dan diagram koneksi komponen
- Troubleshooting kode dan rangkaian microcontroller

## 3.6 Menampilkan Gambar (Contoh: Pinout Arduino)

QuantumBot dapat menampilkan gambar teknis sebagai bagian dari jawaban, misalnya diagram pinout Arduino Uno. Gambar akan ditampilkan langsung di dalam bubble pesan. Jika gambar tidak muncul, pastikan koneksi internet Anda aktif karena gambar dimuat dari sumber eksternal.

[MASUKKAN GAMBAR: Contoh bubble pesan QuantumBot yang memuat gambar pinout Arduino Uno yang ditampilkan di dalam area chat, dengan teks penjelasan di atas atau bawah gambar]

## 3.7 Logout

Untuk keluar dari sistem, klik tombol **Logout** di pojok kanan atas header. Sesi Anda akan dihentikan dan browser akan kembali ke Halaman Login secara otomatis.

---

# BAB 4 — Prosedur Pengoperasian: Panel Admin (Dosen)

## 4.1 Mengenal Antarmuka Panel Admin

[MASUKKAN GAMBAR: Tampilan keseluruhan Panel Admin QuantumBot — header ungu di atas dengan logo, badge "ADMIN", tombol Simpan Perubahan dan Logout, lalu konten halaman yang terdiri dari beberapa kartu/card yang tersusun vertikal]

Panel Admin dapat diakses hanya oleh pengguna dengan peran **Dosen**. Antarmuka ini terdiri dari header navigasi di bagian atas dan sejumlah **kartu (card)** yang masing-masing mengatur aspek berbeda dari sistem. Seluruh kartu dapat diakses dengan melakukan scroll ke bawah.

**Header Panel Admin** memuat logo QuantumBot di sisi kiri, badge bertuliskan **ADMIN**, indikator teks hijau bertuliskan "Perubahan disimpan" yang muncul saat konfigurasi berhasil disimpan, tombol **Simpan Perubahan** berwarna ungu, dan tombol **Logout** di sisi kanan.

## 4.2 Kartu Konfigurasi Bot

[MASUKKAN GAMBAR: Kartu "Konfigurasi Bot" pada Panel Admin — menampilkan area teks besar untuk System Prompt dan dua toggle switch untuk Allow Off-Topic dan Use Pro Model]

Kartu ini mengatur perilaku utama QuantumBot.

**System Prompt** adalah instruksi utama yang membentuk kepribadian dan batasan topik QuantumBot. Anda dapat mengedit teks di area ini untuk menyesuaikan bagaimana bot menjawab pertanyaan. Perubahan akan berlaku pada seluruh sesi percakapan mahasiswa setelah disimpan.

**Toggle Allow Off-Topic:** Jika diaktifkan (posisi ON/biru), bot diizinkan menjawab pertanyaan di luar topik microcontroller. Jika dinonaktifkan (posisi OFF/abu), bot akan menolak pertanyaan di luar topik dengan sopan. Secara default, toggle ini dalam posisi OFF.

**Toggle Use Pro Model:** Jika diaktifkan, sistem akan menggunakan model AI yang lebih canggih dengan kemampuan lebih tinggi. Perhatikan bahwa penggunaan model Pro dapat meningkatkan biaya operasional. Secara default, toggle ini dalam posisi OFF.

Setelah melakukan perubahan, klik tombol **Simpan Perubahan** di header untuk menyimpan konfigurasi.

## 4.3 Kartu Welcome Screen Settings

[MASUKKAN GAMBAR: Kartu "Welcome Screen Settings" — memperlihatkan kolom input untuk Welcome Title, Welcome Description, daftar chip saran yang dapat diedit, dan kolom Google Drive Link]

Kartu ini mengatur tampilan layar sambutan yang dilihat mahasiswa saat pertama kali membuka halaman chat.

**Welcome Title** adalah judul besar yang muncul di welcome screen, seperti "Halo! Saya QuantumBot".

**Welcome Description** adalah teks penjelasan singkat di bawah judul, mendeskripsikan fungsi bot.

**Chip Saran Pertanyaan** adalah daftar pertanyaan contoh yang muncul sebagai tombol di welcome screen. Anda dapat menambah chip baru dengan mengisi kolom dan menekan tombol **+**. Untuk menghapus chip, klik ikon **×** di samping chip yang ingin dihapus.

**Google Drive Link** adalah tautan ke folder Google Drive yang dapat diakses mahasiswa sebagai referensi materi. Isi kolom ini dengan URL folder Drive yang sesuai.

## 4.4 Kartu Upload Materi (Knowledge Base)

[MASUKKAN GAMBAR: Kartu Upload Materi — menampilkan area upload berbentuk kotak putus-putus bertuliskan instruksi drag-and-drop atau klik, beserta daftar file PDF yang sudah terunggah di bawahnya]

Kartu ini memungkinkan Dosen mengunggah materi perkuliahan dalam format PDF agar dapat digunakan oleh QuantumBot sebagai referensi saat menjawab pertanyaan mahasiswa.

**Cara mengunggah materi:**

**Langkah 1:** Klik pada **area upload** (kotak bertanda putus-putus) atau seret file PDF langsung ke area tersebut.

**Langkah 2:** Pilih file PDF dari komputer Anda. Ukuran file maksimum adalah 10 MB. Sistem hanya menerima format PDF.

**Langkah 3:** Setelah file dipilih, nama file akan ditampilkan di area upload. Proses ekstraksi teks akan berjalan otomatis.

**Langkah 4:** Tunggu hingga notifikasi hijau muncul bertuliskan pesan keberhasilan beserta jumlah halaman dan karakter yang berhasil diekstrak.

Daftar file yang sudah terunggah akan ditampilkan di bawah area upload. Untuk menghapus semua materi sekaligus, klik tombol **Hapus Semua Materi**.

[MASUKKAN GAMBAR: Tampilan notifikasi sukses berwarna hijau setelah PDF berhasil diunggah, menampilkan nama file dan jumlah halaman]

## 4.5 Kartu Manajemen Kelas

[MASUKKAN GAMBAR: Kartu Manajemen Kelas — sisi kiri berisi form tambah kelas dengan input nama kelas dan tombol Tambah, sisi kanan menampilkan daftar kelas dengan badge status Aktif/Nonaktif, toggle status, dan tombol hapus]

Kartu ini digunakan untuk membuat dan mengelola kelas perkuliahan. Setiap mahasiswa harus terdaftar dalam satu kelas.

**Menambah Kelas Baru:**

**Langkah 1:** Pada kolom **Nama Kelas**, ketikkan nama kelas yang diinginkan (contoh: "Kelas A 2024").

**Langkah 2:** Klik tombol **Tambah Kelas**. Kelas baru akan muncul di daftar kelas dengan status **Aktif** secara default.

**Mengaktifkan/Menonaktifkan Akses Kelas:**

Setiap kelas memiliki toggle status di sebelah kanannya. Geser toggle ke posisi OFF untuk menutup akses kelas tersebut — seluruh mahasiswa dalam kelas itu tidak akan dapat login. Geser kembali ke ON untuk membuka akses.

[MASUKKAN GAMBAR: Close-up daftar kelas dengan badge berwarna hijau bertuliskan "Aktif" dan badge merah bertuliskan "Nonaktif" pada kelas yang berbeda]

**Menghapus Kelas:**

Klik tombol **Hapus** (ikon merah) di samping nama kelas. Perhatian: menghapus kelas akan menghapus secara permanen semua akun mahasiswa yang terdaftar di kelas tersebut.

> **Catatan Penting:** Kelas Default tidak dapat dihapus karena merupakan kelas bawaan sistem.

## 4.6 Kartu Manajemen User (Mahasiswa)

[MASUKKAN GAMBAR: Kartu Manajemen User — sisi kiri form tambah mahasiswa (kolom username, password, pilih kelas), sisi kanan tabel daftar mahasiswa dengan kolom Username, Kelas, dan tombol Hapus]

Kartu ini digunakan untuk mengelola akun mahasiswa dalam setiap kelas.

**Menambah Akun Mahasiswa:**

**Langkah 1:** Pada kolom **Username**, masukkan username untuk mahasiswa (disarankan menggunakan NIM atau nama singkat tanpa spasi).

**Langkah 2:** Pada kolom **Password**, masukkan password awal untuk akun tersebut.

**Langkah 3:** Pada dropdown **Kelas**, pilih kelas tempat mahasiswa ini terdaftar.

**Langkah 4:** Klik tombol **Tambah User**. Akun baru akan muncul di tabel daftar mahasiswa.

**Melihat Daftar Mahasiswa per Kelas:**

Gunakan dropdown **Filter Kelas** di atas tabel untuk menampilkan mahasiswa dari kelas tertentu saja.

**Menghapus Akun Mahasiswa:**

Klik tombol **Hapus** berwarna merah di kolom aksi pada baris mahasiswa yang ingin dihapus. Konfirmasi penghapusan jika diminta.

**Mereset Semua Mahasiswa dalam Kelas:**

Klik tombol **Reset Semua Mahasiswa Kelas Ini** di bagian bawah kartu untuk menghapus seluruh akun mahasiswa dalam kelas yang sedang dipilih sekaligus. Gunakan fitur ini dengan hati-hati karena tindakan ini tidak dapat dibatalkan.

## 4.7 Kartu Live Monitor Status

[MASUKKAN GAMBAR: Kartu Live Monitor — tabel dengan kolom Username, Kelas, Status (bertanda "Online" hijau atau "Offline" abu), dan di bawah tabel terdapat tombol-tombol kirim suara]

Kartu ini memungkinkan Dosen memantau status kehadiran digital mahasiswa secara real-time selama sesi perkuliahan berlangsung.

**Membaca Status Mahasiswa:**

Tabel menampilkan daftar seluruh mahasiswa beserta status koneksinya. Status **Online** (ditandai dengan warna hijau) berarti mahasiswa sedang aktif membuka halaman chat. Status **Offline** (ditandai dengan warna abu) berarti mahasiswa tidak sedang membuka sistem atau sesi telah berakhir.

Sistem mendeteksi keaktifan berdasarkan sinyal heartbeat yang dikirim browser mahasiswa setiap 30 detik. Mahasiswa dianggap Offline jika tidak ada sinyal selama lebih dari 60 detik.

**Merefresh Status:**

Klik tombol **Refresh** untuk memperbarui tampilan status terbaru dari seluruh mahasiswa.

## 4.8 Fitur Kontrol Suara (Sound Alert)

[MASUKKAN GAMBAR: Bagian bawah Kartu Live Monitor yang menampilkan tombol "Kirim Suara ke Semua" dan tombol kirim individual per baris mahasiswa]

Dosen dapat mengirimkan notifikasi suara (bunyi alert) ke perangkat mahasiswa yang sedang Online untuk menarik perhatian, misalnya untuk memulai kuis atau memberikan pengumuman.

**Mengirim Suara ke Semua Mahasiswa Online:**

Klik tombol **Kirim Suara ke Semua**. Seluruh mahasiswa yang saat ini berstatus Online akan menerima notifikasi suara di perangkat mereka.

**Mengirim Suara ke Mahasiswa Tertentu:**

Klik tombol **Kirim Suara** pada baris mahasiswa yang dituju. Hanya mahasiswa tersebut yang akan menerima notifikasi.

## 4.9 Kartu Log Aktivitas

[MASUKKAN GAMBAR: Kartu Log Aktivitas — tabel tiga kolom (Waktu, Username, Pesan) yang menampilkan riwayat pertanyaan mahasiswa dengan timestamp, beserta tombol "Bersihkan Log" di bawah tabel]

Kartu ini menampilkan riwayat seluruh pertanyaan yang pernah diajukan oleh mahasiswa kepada QuantumBot, beserta informasi waktu dan identitas penanya.

Tabel log memuat kolom **Waktu** (tanggal dan jam pertanyaan diajukan), **Username** (nama akun mahasiswa), dan **Pesan** (isi pertanyaan yang diajukan).

Log menampilkan maksimum 200 entri terbaru. Data ditampilkan dari yang paling baru ke paling lama (urutan terbalik).

Untuk menghapus seluruh log, klik tombol **Bersihkan Log**. Tindakan ini tidak dapat dibatalkan.

## 4.10 Menyimpan Perubahan Konfigurasi

Semua perubahan pada **Konfigurasi Bot** dan **Welcome Screen Settings** baru aktif setelah Anda menekan tombol **Simpan Perubahan** di header halaman. Setelah menekan tombol tersebut, teks hijau bertuliskan "Perubahan disimpan" akan muncul di sebelah tombol sebagai konfirmasi. Perubahan pada **Manajemen Kelas**, **Manajemen User**, dan **Upload Materi** disimpan secara otomatis saat tindakan dilakukan.

---

# BAB 5 — Indikator Visual dan Notifikasi

## 5.1 Indikator Status Koneksi

| Indikator | Tampilan | Arti |
|---|---|---|
| Titik hijau berkedip di header chat | Lingkaran kecil hijau menyala | Sistem aktif dan terhubung |
| Badge "Online" di tabel monitor | Teks "Online" warna hijau | Mahasiswa sedang aktif di halaman chat |
| Badge "Offline" di tabel monitor | Teks "Offline" warna abu-abu | Mahasiswa tidak aktif atau belum login |

## 5.2 Indikator Status Kelas

| Tampilan | Arti |
|---|---|
| Badge hijau "Aktif" | Kelas dapat diakses, mahasiswa bisa login |
| Badge merah "Nonaktif" | Kelas dikunci, mahasiswa tidak dapat login |

## 5.3 Notifikasi Upload Materi

| Warna Notifikasi | Arti |
|---|---|
| Kotak notifikasi **hijau** | File PDF berhasil diunggah dan diproses |
| Kotak notifikasi **merah** | Gagal mengunggah (format salah, ukuran melebihi 10 MB, atau PDF tidak mengandung teks) |

## 5.4 Notifikasi Login

| Tampilan | Arti |
|---|---|
| Kotak merah di bawah tombol Masuk | Pesan error login — baca teks di dalamnya |
| Spinner/loading pada tombol Masuk | Proses autentikasi sedang berjalan |
| Halaman berpindah otomatis | Login berhasil |

## 5.5 Notifikasi Simpan Konfigurasi (Panel Admin)

| Tampilan | Arti |
|---|---|
| Teks hijau "Perubahan disimpan" di header | Konfigurasi berhasil tersimpan ke server |
| Tombol Simpan berwarna abu/disabled | Tidak ada perubahan yang perlu disimpan |

## 5.6 Indikator Respons Bot (Halaman Chat)

| Tampilan | Arti |
|---|---|
| Animasi titik bergerak (typing indicator) | QuantumBot sedang memproses dan menyusun jawaban |
| Teks jawaban muncul bertahap | Jawaban sedang dirender oleh sistem |
| Gambar muncul di dalam bubble | Bot menampilkan gambar teknis sebagai bagian jawaban |

---

# BAB 6 — Troubleshooting Pengguna

## 6.1 Tidak Dapat Login

**Masalah:** Muncul pesan "Username atau password salah" padahal merasa sudah benar.

**Solusi:** Pastikan Caps Lock tidak aktif karena username dan password bersifat case-sensitive. Ketikkan ulang dengan teliti. Jika masih gagal, hubungi Dosen untuk meminta reset password.

---

**Masalah:** Muncul pesan "Akun sedang digunakan di perangkat lain!"

**Solusi:** Tutup semua tab atau browser yang pernah digunakan untuk login dengan akun yang sama. Tunggu sekitar 1–2 menit agar sesi lama berakhir otomatis, kemudian coba login kembali. Jika masih bermasalah, minta Dosen untuk memeriksa status sesi dari Panel Admin.

---

**Masalah:** Muncul pesan "Akses kelas ini sedang ditutup oleh Dosen."

**Solusi:** Dosen telah menonaktifkan akses kelas Anda sementara waktu. Hubungi Dosen untuk meminta kelas dibuka kembali.

---

**Masalah:** Muncul pesan "Terlalu banyak percobaan login."

**Solusi:** Tunggu selama 15 menit sebelum mencoba login kembali. Jangan mencoba login berulang kali karena akan memperpanjang masa pemblokiran.

---

**Masalah:** Muncul pesan "Tidak dapat terhubung ke server."

**Solusi:** Periksa koneksi jaringan Anda. Pastikan Anda terhubung ke jaringan yang sama dengan server QuantumBot. Jika menggunakan WiFi laboratorium, pastikan Anda tidak berpindah ke jaringan lain. Jika masalah berlanjut, hubungi teknisi atau Dosen untuk memeriksa status server.

## 6.2 Masalah pada Halaman Chat

**Masalah:** QuantumBot tidak memberikan jawaban / halaman tidak merespons setelah pesan dikirim.

**Solusi:** Tunggu beberapa saat karena pemrosesan AI memerlukan waktu. Jika lebih dari 30 detik tidak ada respons, coba refresh halaman (F5). Pastikan koneksi internet stabil. Jika masalah terjadi terus-menerus, informasikan ke Dosen karena kemungkinan ada masalah pada server atau API.

---

**Masalah:** QuantumBot menjawab pertanyaan dengan "Maaf, saya tidak dapat membantu dengan topik tersebut" meskipun pertanyaan berkaitan dengan microcontroller.

**Solusi:** Coba perjelas pertanyaan Anda dengan menyebut nama komponen secara spesifik (contoh: "Arduino Uno", "ESP32", "sensor DHT22"). Hindari pertanyaan yang terlalu umum atau ambigu.

---

**Masalah:** Gambar pinout tidak muncul di dalam percakapan.

**Solusi:** Pastikan koneksi internet aktif karena gambar dimuat dari server eksternal. Coba refresh halaman dan ajukan pertanyaan yang sama kembali.

---

**Masalah:** Riwayat percakapan terhapus secara tiba-tiba.

**Solusi:** Riwayat percakapan memang bersifat sementara (tidak tersimpan permanen) dan akan terhapus saat halaman di-refresh atau logout. Jika perlu menyimpan jawaban penting, salin teks jawaban secara manual ke dokumen atau catatan sebelum keluar.

## 6.3 Masalah pada Panel Admin (Dosen)

**Masalah:** Tombol **Simpan Perubahan** tidak merespons atau tampak abu-abu.

**Solusi:** Pastikan ada perubahan yang memang dilakukan pada kolom konfigurasi. Periksa koneksi jaringan. Coba refresh halaman, login ulang, dan lakukan perubahan kembali.

---

**Masalah:** File PDF tidak dapat diunggah.

**Solusi:** Pastikan format file adalah PDF (bukan Word, gambar, atau format lain). Pastikan ukuran file tidak melebihi 10 MB. Pastikan PDF mengandung teks yang dapat disalin (bukan PDF hasil scan gambar tanpa OCR). Jika PDF merupakan hasil scan, lakukan OCR terlebih dahulu menggunakan aplikasi seperti Adobe Acrobat atau layanan online sebelum mengunggah.

---

**Masalah:** Status mahasiswa selalu menampilkan "Offline" padahal mahasiswa sudah login.

**Solusi:** Minta mahasiswa untuk memeriksa apakah halaman chat terbuka dengan benar. Status diperbarui setiap 30 detik — tunggu sekitar 1 menit setelah mahasiswa login sebelum merefresh tabel monitor. Klik tombol **Refresh** pada tabel monitor untuk memperbarui data terbaru.

---

**Masalah:** Notifikasi suara tidak terdengar di perangkat mahasiswa setelah tombol kirim suara ditekan.

**Solusi:** Pastikan mahasiswa berstatus Online (bukan Offline) saat suara dikirim. Minta mahasiswa untuk memeriksa pengaturan volume perangkat mereka. Pastikan browser mahasiswa mengizinkan pemutaran audio otomatis (beberapa browser memblokir audio jika pengguna belum berinteraksi dengan halaman). Mahasiswa dapat mengklik sembarang area di halaman chat untuk mengaktifkan izin audio browser.

---

**Masalah:** Kelas yang baru dibuat tidak muncul di dropdown saat menambah mahasiswa.

**Solusi:** Refresh halaman Panel Admin (F5) untuk memuat ulang daftar kelas terbaru, kemudian coba tambah mahasiswa kembali.

---

*Buku Panduan Pengguna QuantumBot — Versi 1.0 | FT UNY, 2026*
*Untuk pertanyaan teknis lebih lanjut, hubungi pengembang sistem.*
