# Kebijakan keamanan VELYN

## Versi yang didukung

Perbaikan keamanan ditujukan untuk aplikasi web resmi yang sedang berjalan dan
versi stabil Android terbaru yang sudah diterbitkan di
[Releases](https://github.com/theepar/velyn-release/releases).
Versi lama dan build pratinjau tidak dijamin menerima perbaikan. Jika belum ada
rilis Android, belum ada APK publik yang termasuk dalam dukungan ini.

## Melaporkan kerentanan

Gunakan [Report a vulnerability](https://github.com/theepar/velyn-release/security/advisories/new)
untuk mengirim laporan privat kepada pengelola. Masuk ke akun GitHub jika diminta.
Kanal ini menerima temuan pada web, APK resmi, maupun layanan VELYN yang
mendukungnya, meskipun kode sumber aplikasi tidak ada di repositori ini.

Jangan mengirim detail kerentanan melalui issue, komentar, atau pull request
publik. Bug biasa dan usulan fitur dapat disampaikan melalui
[Issues](https://github.com/theepar/velyn-release/issues).

Sertakan informasi berikut agar temuan dapat diperiksa:

- Versi aplikasi atau tanggal pengujian web, browser, dan sistem operasi.
- Komponen atau URL yang terdampak serta prasyarat pengujian.
- Langkah reproduksi dan bukti konsep minimal dengan akun/data uji sendiri.
- Dampak yang mungkin terjadi dan hasil yang diharapkan.
- Log atau tangkapan layar yang sudah disamarkan bila diperlukan.

Jangan menyertakan kode OTP aktif, token sesi, kunci privat, passphrase pemulihan,
isi percakapan pribadi, atau data pengguna lain. Jika tanpa sengaja menemukan
data pengguna lain, hentikan akses dan laporkan lokasi serta jenis datanya tanpa
menyalin atau menyebarkannya.

Pengelola akan menilai dampak, meminta informasi tambahan bila diperlukan, dan
berkoordinasi melalui laporan privat mengenai perbaikan serta publikasi temuan.
Tidak ada janji waktu respons, tenggat perbaikan, atau imbalan bug bounty.

## Batas pengujian

Gunakan akun dan perangkat milik sendiri atau yang pemiliknya telah memberi izin.
Kebijakan ini tidak memberi izin untuk mengakses akun orang lain, mengambil data,
melakukan social engineering, mengirim spam, mengganggu layanan, atau menguji
infrastruktur pihak ketiga. Pengujian yang dapat memengaruhi pengguna lain perlu
disepakati terlebih dahulu melalui kanal privat di atas.

## Batas perlindungan saat ini

Pesan pribadi baru memakai `velyn:v2` (X25519, HKDF-SHA256, AES-256-GCM) dan
lampiran memakai kunci acak per berkas. Namun:

- Metadata perutean, waktu, dan ukuran tetap terlihat oleh server.
- Forward secrecy dan verifikasi kode keamanan antarpengguna belum tersedia.
- Enkripsi end-to-end grup antaranggota belum didukung.
- Riwayat `velyn:v1` menggunakan skema lebih lemah dan hanya didukung untuk dibaca.
- Panggilan web menggunakan DTLS-SRTP bawaan WebRTC, terpisah dari enkripsi pesan.

Rincian penggunaan tersedia di bagian [Privasi dan enkripsi](README.md#privasi-dan-enkripsi).
Kebijakan ini bukan pernyataan bahwa aplikasi bebas dari kerentanan.
