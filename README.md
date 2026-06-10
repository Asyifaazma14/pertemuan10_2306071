# Pertemuan 10 – Implementasi Login Menggunakan Shared Preferences pada Flutter

## Gambaran Umum

Proyek ini merupakan aplikasi Flutter sederhana yang memanfaatkan **Shared Preferences** untuk menyimpan informasi login pengguna secara lokal. Dengan metode ini, pengguna tidak perlu melakukan login berulang kali setiap kali aplikasi dibuka. Selain itu, aplikasi juga dilengkapi fitur logout untuk mengakhiri sesi dan menghapus data yang tersimpan.

---

## Fitur Aplikasi

### Form Login

* Input username
* Input password
* Validasi username tidak boleh kosong
* Validasi username minimal 5 karakter
* Validasi password tidak boleh kosong
* Validasi password minimal 8 karakter

### Penyimpanan Sesi Pengguna

* Menggunakan package Shared Preferences
* Menyimpan status login pengguna
* Menyimpan username yang digunakan saat login

### Halaman Utama (Home)

* Menampilkan username yang tersimpan
* Menampilkan pesan selamat datang
* Menampilkan foto profil pengguna
* Menyediakan tombol logout

### Logout

* Menghapus data yang tersimpan pada Shared Preferences
* Mengarahkan pengguna kembali ke halaman login

---

## Package yang Digunakan

```yaml
dependencies:
  flutter:
    sdk: flutter
  shared_preferences: ^2.2.3
```

## Struktur Folder

```text
lib/
│
├── main.dart
│
└── pages/
    ├── login_page.dart
    └── home_page.dart
```

---

## Alur Kerja Aplikasi

### 1. Proses Login

Pengguna memasukkan username dan password pada form yang tersedia. Sebelum login berhasil, sistem akan melakukan pengecekan terhadap data yang dimasukkan sesuai aturan validasi yang telah ditentukan.

### 2. Menyimpan Data Login

Apabila data yang dimasukkan valid, aplikasi akan menyimpan informasi login ke dalam Shared Preferences, yaitu:

* Status login (`isLogin`)
* Username pengguna (`username`)

### 3. Pemeriksaan Status Login

Ketika aplikasi dijalankan, sistem akan memeriksa data login yang tersimpan.

* Jika nilai `isLogin` bernilai `true`, pengguna langsung diarahkan ke halaman Home.
* Jika nilai `isLogin` bernilai `false`, pengguna akan diarahkan ke halaman Login.

### 4. Logout

Saat tombol logout ditekan, aplikasi akan menghapus seluruh data yang tersimpan pada Shared Preferences dan mengakhiri sesi pengguna. Setelah itu, pengguna akan kembali ke halaman login.

---

## Penggunaan Shared Preferences

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

---

## Tampilan Aplikasi

### Halaman Login

Pada halaman ini tersedia:

* Form username
* Form password
* Tombol login

### Halaman Home

Pada halaman utama ditampilkan:

* Foto profil pengguna
* Username pengguna
* Badge verifikasi
* Tombol logout

---

## Hasil Aplikasi

### Halaman Login dan Home

<img width="1919" height="1199" alt="Cuplikan layar 2026-06-03 224950" src="https://github.com/user-attachments/assets/6c686e79-8f2b-445f-8f12-ca6b7b8e1cc2" />

### Hasil Pengujian

<img width="926" height="430" alt="Screenshot 2026-06-10 145638" src="https://github.com/user-attachments/assets/2ff55b40-e40a-40fb-b7aa-460249fc4ae3" />

---

## Kesimpulan

Aplikasi ini menunjukkan bagaimana Shared Preferences dapat digunakan untuk menyimpan data sederhana secara lokal pada perangkat. Dengan penerapan fitur ini, status login pengguna dapat dipertahankan meskipun aplikasi ditutup, sehingga pengalaman pengguna menjadi lebih praktis dan efisien. Selain itu, fitur logout memungkinkan pengguna menghapus data sesi dan kembali ke halaman login dengan mudah.


## Output
<img width="1919" height="1199" alt="Cuplikan layar 2026-06-03 224950" src="https://github.com/user-attachments/assets/6c686e79-8f2b-445f-8f12-ca6b7b8e1cc2" />
<img width="926" height="430" alt="Screenshot 2026-06-10 145638" src="https://github.com/user-attachments/assets/2ff55b40-e40a-40fb-b7aa-460249fc4ae3" />


Aplikasi ini berhasil mengimplementasikan Shared Preferences untuk menyimpan status login dan data pengguna secara lokal. Dengan adanya Shared Preferences, pengguna dapat tetap masuk ke aplikasi tanpa perlu login kembali setiap kali aplikasi dibuka.
