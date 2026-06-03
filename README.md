# Pertemuan 10 - Flutter Shared Preferences Login

## Deskripsi

Aplikasi Flutter sederhana yang menerapkan sistem login menggunakan Shared Preferences. Data login disimpan secara lokal sehingga pengguna tidak perlu login kembali ketika aplikasi dibuka ulang. Aplikasi juga menyediakan fitur logout untuk menghapus data sesi pengguna.

## Fitur

* Form Login

  * Input Username
  * Input Password
  * Validasi Username tidak boleh kosong
  * Validasi Username minimal 5 karakter
  * Validasi Password tidak boleh kosong
  * Validasi Password minimal 8 karakter

* Penyimpanan Data Login

  * Menggunakan Shared Preferences
  * Menyimpan status login (`isLogin`)
  * Menyimpan username pengguna

* Home Page

  * Menampilkan username yang tersimpan
  * Menampilkan ucapan selamat datang
  * Menampilkan foto profil
  * Tombol Logout

* Logout

  * Menghapus seluruh data Shared Preferences
  * Mengembalikan pengguna ke halaman Login

## Package yang Digunakan

```yaml
dependencies:
  flutter:
    sdk: flutter
  shared_preferences: ^2.2.3
```

## Struktur Project

```text
lib/
│
├── main.dart
│
└── pages/
    ├── login_page.dart
    └── home_page.dart
```

## Cara Kerja Aplikasi

### 1. Login

Pengguna memasukkan username dan password. Sistem akan melakukan validasi sebelum login berhasil.

### 2. Penyimpanan Data

Jika validasi berhasil:

* Status login disimpan dengan key `isLogin`
* Username disimpan dengan key `username`

### 3. Cek Login

Saat aplikasi dijalankan, sistem akan memeriksa nilai `isLogin`.

* Jika bernilai `true`, pengguna langsung masuk ke Home Page.
* Jika bernilai `false`, pengguna diarahkan ke Login Page.

### 4. Logout

Saat tombol logout ditekan:

* Semua data Shared Preferences dihapus.
* Pengguna dikembalikan ke halaman Login.

## Implementasi Shared Preferences

### Menyimpan Data

```dart
await prefs.setBool('isLogin', true);
await prefs.setString('username', usernameController.text);
```

### Mengambil Data

```dart
username = prefs.getString('username') ?? '';
```

### Menghapus Data

```dart
await prefs.clear();
```

## Hasil Aplikasi

### Halaman Login

Menampilkan:

* Input Username
* Input Password
* Tombol Login

### Halaman Home

Menampilkan:

* Foto profil
* Username pengguna
* Badge verified
* Tombol Logout

## Kesimpulan

<img width="1919" height="1199" alt="Cuplikan layar 2026-06-03 224950" src="https://github.com/user-attachments/assets/6c686e79-8f2b-445f-8f12-ca6b7b8e1cc2" />
<img width="1919" height="1199" alt="Cuplikan layar 2026-06-03 225435" src="https://github.com/user-attachments/assets/613c3f81-5aa9-439b-a58c-4e05d84007f0" />

Aplikasi ini berhasil mengimplementasikan Shared Preferences untuk menyimpan status login dan data pengguna secara lokal. Dengan adanya Shared Preferences, pengguna dapat tetap masuk ke aplikasi tanpa perlu login kembali setiap kali aplikasi dibuka.
