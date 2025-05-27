# 📘 Laporan Praktikum Navigasi Flutter

## 🔍 Tujuan Praktikum
Praktikum ini bertujuan untuk memahami serta mengimplementasikan berbagai jenis navigasi dalam aplikasi Flutter.

## 🪐 Gambaran Singkat 4 Jenis Navigasi
1. **Named Routes**
Sistem navigasi yang menggunakan string identifier (seperti '/home', '/detail') untuk       berpindah antar layar. Memiliki keunggulan berupa route yagn terpusat, mudah dimaintain, dan mendukung deep linking.
2. **Navigator 2.0**
Merupakan sistem navigasi deklaratif yang lebih modern yang dapat memberikan full control terhadap navigation stack dan state management.
3. **Nested Navigation**
Merupakan istem navigasi bertingkat yang memungkinkan beberapa navigator bekerja dalam satu aplikasi, misalnya tab naivagtion dengan sub-navigation di setiap tab.
4. **Deep Linking**
Merupakan navigasi yang memungkinkan pengguna mengakses layar tertentu secara langsung lewat URL.

## 1️⃣ Navigation (Named Routes)
### Deskripsi Aplikasi
Aplikasi terdiri dari 3 layar utama dengan konfigurasi routes berikut:
```
routes: {
  '/': (context) => const HomeScreen(),
  '/detail': (context) => const DetailScreen(data: 'Hello from Home!'),
  '/settings': (context) => const SettingsScreen(username: 'Guest'),
}
```

### Screenshot dan Penjelasan Aplikasi
**1. HomeScreen**

<p align="center">
  <img src="https://github.com/user-attachments/assets/bfdcc402-d2f6-45d9-8430-1270065ca43c" width="45%" />
</p>

**Widget Utama** 

Scaffold, Appbar, Column, Elevatedbutton, SizdeBox

**Fungsi Navigasi**

- Push Navigation: Navigator.push() dengan MaterialPageRoute
- Named Route: Navigator.pushNamed(context, '/detail');
- Named Route + Arguments: Navigator.pushNamed(context, '/settings', arguments: 'John Doe')

**2. Detail Screen**

<p align="center">
  <img src="https://github.com/user-attachments/assets/d37470b0-4bd8-4d2b-9ea5-ab8eb9f9c990" width="45%" />
  <img src="https://github.com/user-attachments/assets/79fc026a-f570-42db-8c46-8059b73e01be" width="45%" />
</p>

**Widget Utama**

Scaffold, AppBar, Text, ElevatedButton

**Cara Menerima Data**

Melalui constructor parameter dan menampilkan sdengan string interpolation

**3. SettingScreen**

<p align="center">
  <img src="https://github.com/user-attachments/assets/b0e811ee-0022-41f7-a2a8-0fe6916357fb" width="45%" />
</p>

**Widget Utama**

Scaffold, Appbar, Text, ElevatedButton

**Fitur Khusus**

Menerima arguments dari named route menggunakan 

```
ModalRoute.of(context)?.settings.arguments
```
pada variabel args

****
### Modifikasi Kode

Dilakukan penambahan halaman About dengan tampilan berikut:

<p align="center">
  <img src="https://github.com/user-attachments/assets/3de84d7e-5c6a-4413-b032-80ec07416a5e" width="45%" />
  <img src="https://github.com/user-attachments/assets/e400e7a0-cd87-4183-bcaf-d487da240c10" width="45%" />
</p>

**Modifikasi yang Ditambahkan pada About:**

**1. Route Baru di MaterialApp**
```
'/about': (context) => const AboutScreen(),
```

**2. Tombol Navigasi di Home Screen**

Menggunakan navigator Push Name yang mengarah ke /about
```
Navigator.pushNamed(context, '/about');
```

**3. Kemampuan Navigasi**

Ke DetailScreen via named route, ke SettingScreen dengan argument "About User", kembali ke HomeScreen dengan Navigator.pop()

## 2️⃣ Navigation 2.0
### Deskripsi Aplikasi
Aplikasi menggunakan navigator 2.0 dengan pendekatan deklaratif untuk mengelola navigation stack berdasarkan state aplikasi. 

**Konsep Utama: **

- StatefulWidget sebagai root dengan state management
- Navigator dengan pages array yang didefinisikan secara deklaratif
- Navigation berdasarkan perubahan state, bukan imperative calls

### Screenshot dan Penjelasan
**1. HomeScreen**

<p align="center">
  <img src="https://github.com/user-attachments/assets/fe168974-fb76-44bc-9f12-c33d72c15ce9" width="45%" />
</p>

**Widget Utama**

Scaffold, AppBar, ListView.builder, ListTile

**Fitur Navigasi**

Navigasi terjadi melalui callback onItemSelected() yang memanggil fungsi _selectItem(item) untuk mengubah state _selectedItem. Perubahan state ini menyebabkan DetailScreen ditambahkan ke dalam list pages.

**2. DetailScreen**

<p align="center">
  <img src="https://github.com/user-attachments/assets/b3a3e696-7de4-4666-8d9d-a0b1a6b60ca2" width="33%" />
  <img src="https://github.com/user-attachments/assets/c0b55d89-2efb-43eb-8d56-c771f56f1094" width="33%" />
  <img src="https://github.com/user-attachments/assets/cb89dcfd-cbc4-4b70-9811-3e69cf554824" width="33%" />
</p>

**Widget Utama**

Scaffold, AppBar, column, text, elevatedbutton

**Fitur Navigasi**

Terdapat tombol back yang memanggil callback onBack(), yang kemudian mengubah state _selectedItem = null. Ini menghapus DetailScreen dari list pages.

### Modifikasi Kode
Dilakukan penambahan field 'tugasPrakPBM' yang kemudian ditampilkan baik pada homescreen maupun detailscreen.

<p align="center">
  <img src="https://github.com/user-attachments/assets/0e124ddb-ec6a-4f68-9106-2e1caff08dde" width="40%" />
  <img src="https://github.com/user-attachments/assets/1c9563d6-1e93-482d-9623-d50531bdf65e" width="40%" />
  <img src="https://github.com/user-attachments/assets/a8e824d7-3621-489a-8fa0-2aaa6b74998e" width="40%" />
  <img src="https://github.com/user-attachments/assets/fc607348-4f3e-47c7-a340-3410dd928a86" width="40%" />
</p>

- Dilakukan penambahan atribut tugasPrakPBM berupa string yang kemudian ditambahkan ke constructor juga
  
```
class Item {
  final int id;
  final String name;
  final String tugasPrakPBM; // New field

  Item({
    required this.id,
    required this.name,
    required this.tugasPrakPBM, // Add to constructor
  });
}
```

- Menambahkan tugasPrakPBM pada isi list
- Menambahkan dan memanggil variabel tugasPrakPBM pada Children di HomeScreen dan DetailScreen

### Alur Navigasi
1. Aplikasi dijalankan → `MyApp` menginisialisasi `MyRouterDelegate` dan `MyRouteInformationParser`
2. `MyRouterDelegate` membaca state `_selectedItem`
3. Jika `_selectedItem == null`, hanya `HomeScreen` dimunculkan
4. Jika user memilih item:
   - Fungsi `onItemTapped(item)` → `_selectItem(item)` → set state `_selectedItem = item`
   - `notifyListeners()` memicu `Navigator` rebuild dengan menambahkan `DetailScreen`
5. Jika user tekan tombol "Kembali":
   - `onBack()` → set `_selectedItem = null`
   - `DetailScreen` dikeluarkan dari stack

## 3️⃣. Nested Navigation
### Deskripsi Aplikasi 
Aplikasi yang terdapat navigasi bersarang didalamnya. Ini berguna untuk membuat jalur tertentu yang mengarahkan pengguna ke halamannya masing-masing.

### Screenshot dan Penjelasan
**1. HomeScreen**

![image](https://github.com/user-attachments/assets/77e0d221-fa74-4407-99cc-d1965415f800)

**Widget Utama**

Scaffold, AppBar, column, text, elevatedbutton

**Fitur Navigasi**
Navigasi terjadi melalui ElevatedButton dengan navigator push yang mengarahkan ke SetupFlowScreen

### Modifikasi Kode

## 4️⃣ Deep Link Navigation
### Deskripsi Aplikasi

### Screenshot dan Penjelasan

### Modifikasi Kode

