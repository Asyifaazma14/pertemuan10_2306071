# Pertemuan 10 – Implementasi Login dan Manajemen Produk Menggunakan Shared Preferences pada Flutter

## Gambaran Umum

Proyek ini merupakan aplikasi Flutter yang memanfaatkan **Shared Preferences** sebagai media penyimpanan data lokal secara persisten. Selain digunakan untuk menyimpan status login pengguna, aplikasi ini juga menyediakan fitur **Manajemen Produk (CRUD)** yang memungkinkan pengguna menambah, melihat, mengubah, dan menghapus data produk yang tersimpan langsung pada perangkat.

---

## Fitur Utama Aplikasi

### 1. Sistem Login dan Logout

* Form login dengan input username dan password.
* Validasi username tidak boleh kosong dan minimal 5 karakter.
* Validasi password tidak boleh kosong dan minimal 8 karakter.
* Menyimpan status login menggunakan Shared Preferences.
* Menyimpan username pengguna yang berhasil login.
* Logout untuk menghapus data sesi dan kembali ke halaman login.

### 2. Manajemen Produk (CRUD)

* **Create**: Menambahkan produk baru.
* **Read**: Menampilkan daftar produk yang tersimpan.
* **Update**: Mengubah data produk yang sudah ada.
* **Delete**: Menghapus produk dari daftar.

### 3. Validasi Data Produk

* Nama produk wajib diisi.
* Deskripsi produk wajib diisi.
* Harga produk wajib berupa angka.
* Tersedia tombol **Batal** untuk membatalkan proses input.

---

## Package yang Digunakan

```yaml
dependencies:
  flutter:
    sdk: flutter
  shared_preferences: ^2.2.3
```

---

## Struktur Folder Proyek

```text
lib/
│
├── main.dart
├── models/
│   └── product_model.dart
│
└── pages/
    ├── login_page.dart
    └── home_page.dart
```

---

## Alur Kerja Aplikasi

### 1. Proses Login

Pengguna memasukkan username dan password pada halaman login. Jika data yang dimasukkan memenuhi aturan validasi, maka sistem akan menyimpan status login dan username ke dalam Shared Preferences.

### 2. Penyimpanan Data Sesi

Data yang disimpan meliputi:

* `isLogin`
* `username`

Saat aplikasi dibuka kembali, sistem akan memeriksa status login yang tersimpan.

### 3. Pengelolaan Produk

Data produk disimpan menggunakan Shared Preferences dalam bentuk `List<String>`. Setiap objek produk akan dikonversi ke format JSON sebelum disimpan dan dikembalikan menjadi objek saat dibaca kembali.

### 4. Logout

Ketika tombol logout ditekan, seluruh data yang tersimpan akan dihapus dan pengguna akan diarahkan kembali ke halaman login.

---

## Implementasi Shared Preferences

### Menyimpan Data Login

```dart
await prefs.setBool('isLogin', true);
await prefs.setString('username', usernameController.text);
```

### Mengambil Data Username

```dart
username = prefs.getString('username') ?? '';
```

### Menyimpan Data Produk

```dart
Future<void> saveProducts() async {
  final prefs = await SharedPreferences.getInstance();

  List<String> productList =
      products.map((item) => item.toJson()).toList();

  await prefs.setStringList('products', productList);
}
```

### Memuat Data Produk

```dart
Future<void> loadProducts() async {
  final prefs = await SharedPreferences.getInstance();

  final productList =
      prefs.getStringList('products') ?? [];

  setState(() {
    products = productList
        .map((item) => ProductModel.fromJson(item))
        .toList();
  });
}
```

### Menghapus Data

```dart
await prefs.clear();
```

---

## Tampilan Aplikasi

### Halaman Login

Halaman login menyediakan:

* Input username
* Input password
* Tombol login
* Validasi form

### Halaman Home

Halaman utama menampilkan:

* Foto profil pengguna
* Nama pengguna
* Badge verifikasi
* Tombol logout
* Daftar produk
* Tombol tambah produk
* Tombol edit produk
* Tombol hapus produk

---

### Halaman Login dan Home



<img width="1919" height="1199" alt="Cuplikan layar 2026-06-03 224950" src="https://github.com/user-attachments/assets/6c686e79-8f2b-445f-8f12-ca6b7b8e1cc2" />



### Hasil Pengujian



<img width="926" height="430" alt="Screenshot 2026-06-10 145638" src="https://github.com/user-attachments/assets/2ff55b40-e40a-40fb-b7aa-460249fc4ae3" />

<img width="929" height="1002" alt="Screenshot 2026-06-10 161850" src="https://github.com/user-attachments/assets/e3620ca9-3d80-4eb4-890c-8aac807eecfa" />

<img width="932" height="999" alt="Screenshot 2026-06-10 161921" src="https://github.com/user-attachments/assets/d44f82ea-9649-45f4-bdc2-d746d3a993a2" />

<img width="930" height="1007" alt="Screenshot 2026-06-10 161911" src="https://github.com/user-attachments/assets/0acc9212-8678-462b-9dfa-879fea3a295b" />

<img width="924" height="997" alt="Screenshot 2026-06-10 161901" src="https://github.com/user-attachments/assets/feb2bd85-2e30-41a9-b05c-05f69fa080d8" />

---

## Kesimpulan

Aplikasi ini berhasil mengimplementasikan Shared Preferences untuk menyimpan data login dan data produk secara lokal. Selain menjaga sesi login pengguna tetap aktif, aplikasi juga mampu melakukan pengelolaan data produk menggunakan operasi CRUD yang tersimpan secara persisten pada perangkat. Dengan kombinasi validasi form dan penyimpanan lokal, aplikasi dapat memberikan pengalaman penggunaan yang lebih praktis, ringan, dan mudah digunakan.
