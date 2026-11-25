# We's Gym — Android project

Aplikasi offline-first berbasis HTML/CSS/JavaScript, dibungkus menjadi Android app menggunakan Capacitor. Data disimpan lokal di WebView (`localStorage`); tidak ada akun/server.

## Fitur
- Dua profil terpisah (We dan My), mengikuti jadwal latihan dari versi HTML awal.
- Checklist latihan per tanggal dan hari program.
- Workout log: gerakan, set, repetisi, beban, RPE opsional, catatan.
- Riwayat sesi dan statistik sederhana.
- Grafik beban tercatat per gerakan.
- Exercise library, rest timer, backup/restore JSON.
- Pengingat notifikasi lokal Android berdasarkan hari dan jam pilihan.

## Build APK gratis melalui GitHub Actions (tanpa Android Studio)

1. Buat repository baru di GitHub dan unggah seluruh isi folder proyek ini (termasuk folder tersembunyi `.github/workflows`).
2. Pastikan nama branch utama adalah `main`.
3. Buka tab **Actions** pada repository dan aktifkan Actions jika diminta.
4. Pilih workflow **Build We's Gym APK**.
5. Tekan **Run workflow**. Kamu juga bisa menjalankannya otomatis setiap kali melakukan push ke branch `main`.
6. Tunggu sampai workflow selesai dengan status hijau.
7. Buka hasil run, cari bagian **Artifacts**, lalu unduh `wes-gym-debug-apk`.
8. Ekstrak ZIP artifact dan instal `app-debug.apk` di HP Android. Jika Android meminta izin instalasi dari sumber tersebut, izinkan untuk aplikasi/browser yang kamu gunakan.

Workflow menggunakan GitHub-hosted runner untuk memasang Node.js, Java, Android SDK, membangun aset web, menambahkan platform Android Capacitor, lalu menjalankan Gradle. Tidak diperlukan Android Studio di HP atau PC.

## Biaya dan batas penggunaan

GitHub Actions dapat digunakan tanpa biaya selama penggunaan masih dalam kuota paket akun/repository. Batas kuota dan kebijakan GitHub dapat berubah; cek halaman billing/usage akun GitHub. Jangan mengaktifkan paid spending atau menambahkan metode pembayaran jika ingin menjaga biaya tetap Rp0.

## Build lokal (opsional)

Persyaratan: Node.js LTS, Java 21, Android SDK, dan Gradle wrapper yang dibuat oleh Capacitor. Android Studio tidak wajib jika SDK dan tools command-line sudah tersedia, tetapi pengaturan lokalnya lebih rumit.

```bash
npm install
npm run build
npx cap add android
npx cap sync android
cd android
./gradlew assembleDebug
```

APK debug biasanya berada di `android/app/build/outputs/apk/debug/app-debug.apk`.

## Notifikasi
- Pengingat terjadwal menggunakan plugin Capacitor Local Notifications dan hanya tersedia di aplikasi Android native; preview browser biasa tidak menjamin notifikasi terjadwal.
- Buka Settings > Notifikasi latihan, aktifkan, pilih jam dan hari, lalu Simpan.
- Izinkan notifikasi saat Android meminta izin. Android 13+ memerlukan izin notifikasi.
- Perangkat dapat menerapkan pembatasan baterai/alarm. Uji pengingat pada perangkat target. Pengingat ini bukan alarm medis/kritis.

## Penyimpanan & backup
Data berada di penyimpanan lokal aplikasi. Hapus data aplikasi/uninstall dapat menghapus data; ekspor backup JSON secara berkala. Impor backup mengganti data dua profil yang ada.

## Catatan pengujian
JavaScript dapat diperiksa secara statis, tetapi APK tetap harus dibangun dan diuji pada HP Android target. Keberhasilan build cloud tidak otomatis menjamin semua fitur bekerja di setiap perangkat atau versi Android.
