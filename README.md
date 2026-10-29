<div align="center">

<img src="assets/velyn-v-purple.svg" alt="Logo VELYN" width="88" height="88" />

# VELYN

**Tetap dekat, di mana saja.**

Perpesanan real-time dengan enkripsi end-to-end untuk percakapan pribadi,
serta panggilan suara dan video melalui web.

[Buka aplikasi](https://chat.velynchat.web.id/) · [Situs resmi](https://www.velynchat.web.id/) · [Rilis](https://github.com/theepar/velyn-release/releases)

</div>

Repositori ini menyediakan informasi penggunaan, catatan rilis, dan distribusi
aplikasi VELYN. Kode sumber aplikasi bersifat proprietary dan tidak dipublikasikan
di repositori ini.

> **Ketersediaan:** aplikasi web dapat digunakan sekarang. Per 29 Oktober 2026,
> belum ada rilis atau APK Android yang dipublikasikan di repositori ini.

## Daftar isi

- [Mulai menggunakan VELYN](#mulai-menggunakan-velyn)
- [Fitur dan dukungan platform](#fitur-dan-dukungan-platform)
- [Privasi dan enkripsi](#privasi-dan-enkripsi)
- [Pindah ke perangkat baru](#pindah-ke-perangkat-baru)
- [Bantuan dan masukan](#bantuan-dan-masukan)
- [Lisensi](#lisensi)

## Mulai menggunakan VELYN

### Web

1. Buka [chat.velynchat.web.id](https://chat.velynchat.web.id/) dari browser terbaru
   di komputer atau ponsel.
2. Masukkan alamat email, lalu gunakan kode verifikasi yang dikirim ke kotak masuk.
3. Lengkapi profil jika diminta, lalu mulai percakapan.

Untuk panggilan suara atau video, izinkan akses mikrofon dan kamera saat diminta.
Kualitas panggilan bergantung pada perangkat, izin browser, dan jaringan kedua
pengguna. Browser juga perlu mendukung Web Crypto X25519 agar enkripsi pesan
dapat digunakan.

Versi web digunakan langsung di browser. VELYN saat ini tidak menyediakan PWA
atau aplikasi desktop native.

### Android

Klien Android dikembangkan dengan Flutter. APK akan tersedia melalui halaman
[Releases](https://github.com/theepar/velyn-release/releases) saat dipublikasikan.

Setelah APK tersedia:

1. Buka rilis yang ingin dipasang dan unduh berkas APK pada bagian **Assets**.
2. Buka berkas tersebut. Jika diminta Android, izinkan pemasangan dari aplikasi
   browser atau pengelola berkas yang digunakan.
3. Selesaikan pemasangan, lalu masuk dengan akun VELYN.

Fitur klien Android belum setara dengan web. Panggilan suara dan video belum
didukung di aplikasi Android.

## Fitur dan dukungan platform

VELYN mendukung percakapan pribadi real-time, indikator sedang mengetik,
status pesan, dan penautan perangkat melalui QR. Perbedaan implementasi klien
saat ini dirangkum di bawah; ketersediaan pada APK mengikuti versi yang dirilis.

| Fitur | Web | Klien Android |
| :--- | :--- | :--- |
| Masuk dengan kode verifikasi email | Didukung | Didukung |
| Pesan pribadi terenkripsi end-to-end | Didukung | Didukung |
| Mengirim lampiran terenkripsi | Gambar, video, audio, dan dokumen | Gambar dari galeri atau kamera |
| Menerima dan membuka lampiran terenkripsi | Didukung | Didukung |
| Panggilan suara dan video | WebRTC | Belum didukung |

Nomor akun privat berbeda dari username. Nomor tersebut berupa 12 digit acak
dan hanya ditampilkan pada profil pemilik akun di pengaturan; nomor ini tidak
ditampilkan kepada kontak lain.

## Privasi dan enkripsi

Pesan pribadi baru memakai skema `velyn:v2`: pertukaran kunci **X25519**, penurunan
kunci **HKDF-SHA256**, dan enkripsi **AES-256-GCM**. Isi pesan dienkripsi di
perangkat sebelum dikirim, lalu disimpan di server dalam bentuk ciphertext.
Jika kunci belum tersedia, pesan gagal dikirim tanpa beralih ke teks terbuka.

Lampiran dienkripsi dengan kunci acak per berkas. Kunci untuk membuka lampiran
disertakan di dalam pesan yang terenkripsi. Panggilan web menggunakan
perlindungan media **DTLS-SRTP** bawaan WebRTC; koneksi dapat berlangsung langsung
antarperangkat atau melalui relay TURN sesuai kondisi jaringan.

Ada beberapa batasan yang perlu dipahami:

- **Metadata tetap terlihat oleh server**, termasuk identitas pengirim dan
  penerima, waktu, serta ukuran pesan.
- **Forward secrecy belum tersedia.** Skema saat ini menggunakan kunci akun
  agar riwayat dapat dibuka di perangkat lain yang memiliki kunci tersebut.
- **Enkripsi grup antaranggota belum didukung.** Penjelasan enkripsi end-to-end
  di atas berlaku untuk percakapan pribadi.
- **Verifikasi kode keamanan antarpengguna belum tersedia.** Distribusi kunci
  publik masih bergantung pada server.
- **Riwayat lama `velyn:v1` memiliki skema perlindungan yang lebih lemah.**
  Format tersebut hanya dipertahankan untuk membaca pesan lama, bukan untuk
  mengirim pesan baru.

## Pindah ke perangkat baru

Masuk dengan email yang sama memulihkan akses akun, tetapi perangkat baru juga
memerlukan kunci enkripsi untuk membuka riwayat pesan.

- **Melalui QR:** tampilkan QR masuk pada perangkat baru, lalu pindai dan setujui
  dari perangkat lama yang sudah masuk dan memiliki kunci akun. Kunci
  dipindahkan dalam bentuk terenkripsi.
- **Melalui passphrase pemulihan:** gunakan passphrase jika sebelumnya sudah
  membuat cadangan pemulihan kunci.

Jika perangkat lama dan passphrase pemulihan tidak tersedia, Anda dapat membuat
kunci baru untuk melanjutkan percakapan. Riwayat yang memakai kunci lama tidak
dapat dibuka dengan kunci baru. Simpan akses ke perangkat lama sampai penautan
perangkat baru selesai.

## Bantuan dan masukan

Laporkan bug atau usulkan fitur melalui
[GitHub Issues](https://github.com/theepar/velyn-release/issues). Sertakan versi
aplikasi, perangkat atau browser, langkah reproduksi, dan tangkapan layar jika
diperlukan. Hindari menyertakan isi percakapan pribadi, kode OTP, token sesi,
atau passphrase pemulihan.

Untuk laporan kerentanan keamanan, gunakan
[Report a vulnerability](https://github.com/theepar/velyn-release/security/advisories/new)
secara privat. Panduan pelaporan dan cakupan dukungan ada di [SECURITY.md](SECURITY.md).

## Lisensi

VELYN merupakan perangkat lunak proprietary. Repositori publik ini digunakan
untuk dokumentasi dan distribusi rilis; ketersediaannya tidak memberikan lisensi
open-source atas kode sumber aplikasi.

Izin penggunaan aplikasi dan batas penggunaan materi tersedia di [LICENSE.md](LICENSE.md).

Copyright © 2026 VELYN Team.
