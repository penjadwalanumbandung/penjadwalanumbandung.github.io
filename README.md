
1. Pendahuluan
UMB Manager v1.7 adalah aplikasi berbasis web (Single Page Application) yang dirancang khusus untuk mengelola jadwal perkuliahan secara dinamis. Aplikasi ini memfasilitasi administrasi jadwal seperti pemindahan jam kuliah, penukaran jadwal antar dosen, serta pemantauan ketersediaan ruangan secara real-time berbasis data statis dari Excel.

2. Arsitektur Teknologi

Aplikasi ini dibangun menggunakan teknologi modern tanpa memerlukan backend server tradisional, memanfaatkan penyimpanan lokal browser:
Frontend Framework: React 18 (via ESM)
Styling: Tailwind CSS (Utilitas UI responsif)
Icons: Lucide-React
Data Processing: SheetJS (XLSX) untuk membaca dan membuat file Excel.
Transpiler: Babel (untuk menjalankan JSX di browser).
Persistence: LocalStorage API.

3. Fitur Utama

A. Dashboard Jadwal
Visualisasi Kartu: Menampilkan jadwal dalam bentuk kartu yang informatif (Mata Kuliah, Dosen, Kelas, SKS, Semester, Hari, Waktu, dan Ruangan).
Filter & Pencarian: Fitur pencarian global yang mencakup semua kolom data.
Sorting Cerdas: Pengurutan berdasarkan Hari (sesuai urutan Senin-Sabtu), Mata Kuliah, Dosen, atau Ruangan.
Riwayat Cepat: Menampilkan catatan perubahan terakhir langsung pada kartu jadwal jika jadwal tersebut pernah diubah.

B. Cari Ruang Kosong (Scanner)
Memungkinkan pengguna memilih Hari dan Jam tertentu.
Sistem akan membagi ruangan menjadi dua kategori:
Tersedia: Ruangan yang tidak digunakan pada slot waktu tersebut.
Terisi: Ruangan yang sedang digunakan, lengkap dengan detail mata kuliah dan dosen yang sedang mengajar.

C. Tukar & Pindah (Swap & Move)
Fitur paling kompleks yang dilengkapi dengan Collision Detection (Deteksi Tabrakan):
Advanced Swap: Menukar jadwal Dosen A dengan Dosen B. Sistem secara otomatis memvalidasi apakah penukaran tersebut akan menyebabkan jadwal bentrok bagi dosen atau kelas yang bersangkutan.
Move to Empty Slot: Memindahkan jadwal ke ruangan dan jam yang benar-benar kosong di hari tujuan.

D. Riwayat & Berita Acara (Audit Log)
Setiap perubahan jadwal wajib menyertakan alasan (Berita Acara).
Fitur Undo: Tombol satu klik untuk mengembalikan perubahan ke status sebelumnya jika terjadi kesalahan input.

E. Manajemen Data
Import Excel: Mengunggah file .xlsx untuk mengisi database awal.
Export Excel: Mengunduh jadwal yang sudah diperbarui kembali ke file Excel.
Persistence: Data tersimpan secara permanen di browser pengguna melalui localStorage.

4. Logika Bisnis (Collision Detection)
Sistem keamanan data memastikan tidak ada jadwal yang bentrok dengan aturan:
Dosen: Seorang dosen tidak boleh mengajar di dua kelas/ruang berbeda pada waktu yang sama.
Kelas: Sebuah rombel/kelas tidak boleh memiliki dua mata kuliah berbeda di jam yang sama.
Ruangan: Satu ruangan tidak boleh digunakan oleh dua mata kuliah berbeda di jam yang sama.
Logika ini dijalankan menggunakan fungsi isOverlap yang membandingkan rentang menit (start - end) dari setiap slot waktu.

5. Konfigurasi Penyimpanan (Storage)
Aplikasi menggunakan kunci penyimpanan berikut di LocalStorage:
umb_schedule_v8_7: Menyimpan array objek jadwal.
umb_history_v8_7: Menyimpan log aktivitas/audit trail.
umb_admin_v8_7: Menyimpan nama notulis/admin aktif.
umb_theme_dark: Menyimpan preferensi tema (Light/Dark mode).

6. Panduan Penggunaan Singkat
Persiapan: Buka aplikasi dan klik tombol "Impor Excel" untuk memasukkan data jadwal awal.
Identitas: Atur nama Notulis pada sidebar untuk keperluan Berita Acara.
Pencarian: Gunakan kolom pencarian di header untuk memfilter jadwal secara instan.
Perubahan: Masuk ke menu "Tukar & Pindah", pilih dosen, pilih matkul, masukkan alasan, dan pilih target penukaran yang divalidasi sistem (berwarna hijau).
Output: Klik "Ekspor Hasil" untuk mendapatkan file Excel terbaru yang siap didistribusikan.
Cetak: Gunakan tombol "Cetak Laporan" untuk mendapatkan format PDF/Cetak fisik berstandar A4 yang rapi.

7. Catatan Versi (v1.7)
Optimalisasi fitur Undo pada riwayat.
Penambahan fitur pencarian pada daftar ruangan yang terisi.
Perbaikan urutan hari pada kandidat penukaran jadwal.
Peningkatan akurasi deteksi bentrok jam kuliah. -->
