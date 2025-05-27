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

Menampilkan tombol "Start Setup" untuk memulai alur setup.

<p align="center">
  <img src="https://github.com/user-attachments/assets/77e0d221-fa74-4407-99cc-d1965415f800" width="45%" />
</p>

**Widget Utama**  
`Scaffold`, `AppBar`, `Column`, `Text`, `ElevatedButton`

**Fungsi Navigasi**

```
dart
ElevatedButton(
  onPressed: () {
    Navigator.of(context).push(
      MaterialPageRoute(builder: (_) => const SetupFlowScreen()),
    );
  },
  child: const Text('Start Setup'),
)
```

**2. Setup Flow Screen**

Berfungsi sebagai navigator untuk mengatur alur nestednya

**Widget Utama**  
Scaffold, AppBar, Navigator, GlobalKey, onGenerateRoute

**Fungsi Navigasi**

```
Navigator(
        key: _navigatorKey,
        initialRoute: 'find_devices',
        onGenerateRoute: (settings) {
          Widget page;
          switch (settings.name) {
            case 'find_devices':
              page = FindDevicesScreen(onDeviceFound: _onDeviceFound);
              break;
            case 'connect_device':
              page = ConnectDeviceScreen(
                onSetupComplete: () {
                  _navigatorKey.currentState!.pushNamed('confirm_device');
                },
              );
              break;
            case 'confirm_device':
              page = ConfirmDeviceScreen(onDone: () => _completeSetup(context));
              break;
            default:
              page = const Center(child: Text('Unknown Route'));
          }
          return MaterialPageRoute(builder: (_) => page);
        },
      )
```

**3. Sub Layar 1-2**
Layar Nested Navigation

<p align="center">
  <img src="https://github.com/user-attachments/assets/02486c4e-d080-44b1-9806-66ddf49f15e0" width="45%" />
  <img src="https://github.com/user-attachments/assets/1352464d-2756-4338-9899-e31b7e05c3ae" width="45%" />
</p>


**Widget Utama**  
Scaffold, AppBar, Text, ElevatedButton

**Fungsi Navigasi**
Navigasi maju sub layar 1 ke sub layar 2
```
  void _onDeviceFound() {
    _navigatorKey.currentState!.pushNamed('connect_device');
  }
```

Navigasi kembali sub layar 2 ke sub layar 1
```
  void _completeSetup(BuildContext context) {
    Navigator.pop(context); // Kembali ke HomeScreen
  }
```

### Modifikasi Kode
Dilakukan penambahan sub layar ke-3 seperti gambar berikut

<p align="center">
  <img src="https://github.com/user-attachments/assets/6e9530ec-a2e1-4ad9-a563-66344cf714b9" width="45%" />
</p>

Kode sub layar ke-3

```
class ConfirmDeviceScreen extends StatelessWidget {
  final VoidCallback onDone;
  const ConfirmDeviceScreen({super.key, required this.onDone});

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      body: Center(
        child: Column(
          mainAxisAlignment: MainAxisAlignment.center,
          children: [
            const Text(
              'Confirm Device',
              style: TextStyle(fontSize: 20, fontWeight: FontWeight.bold),
            ),
            const SizedBox(height: 20),
            ElevatedButton(onPressed: onDone, child: const Text('Done')),
            const SizedBox(height: 10),
            ElevatedButton(
              onPressed: () {
                Navigator.pop(context);
              },
              style: ElevatedButton.styleFrom(
                padding: const EdgeInsets.symmetric(
                  horizontal: 30,
                  vertical: 15,
                ),
                textStyle: const TextStyle(fontSize: 16),
              ),
              child: const Text('Back'),
            ),
          ],
        ),
      ),
    );
  }
}
```

Lalu penambahan rute navigator
```
Navigator(
        key: _navigatorKey,
        initialRoute: 'find_devices',
        onGenerateRoute: (settings) {
          Widget page;
          switch (settings.name) {
            case 'find_devices':
              page = FindDevicesScreen(onDeviceFound: _onDeviceFound);
              break;
            case 'connect_device':
              page = ConnectDeviceScreen(
                onSetupComplete: () {
                  _navigatorKey.currentState!.pushNamed('confirm_device');
                },
              );
              break;
            case 'confirm_device':
              page = ConfirmDeviceScreen(onDone: () => _completeSetup(context));
              break;
            default:
              page = const Center(child: Text('Unknown Route'));
          }
          return MaterialPageRoute(builder: (_) => page);
        },
      ),
```

Dan beberapa perubahan kecil lainnya.

### Alur Navigasi
1. Aplikasi dimulai dan menampilkan HomeScreen.
2. User menekan tombol → Navigasi berpindah ke SetupFlowScreen.
3. Navigator lokal memuat halaman / (Step1), dilanjut ke Step2, Step3, dan Confirm.
4. Setelah menekan "Finish" di ConfirmScreen, user kembali ke HomeScreen menggunakan navigator root.

## 4️⃣ Deep Link Navigation
### Deskripsi Aplikasi
Pada aplikasi ini, deep link digunakan untuk langsung membuka `DetailScreen` berdasarkan parameter yang dibaca dari URI.

### Screenshot dan Penjelasan

**1. HomeScreen**

<p align="center">
  <img src="https://github.com/user-attachments/assets/e72ea1b4-29c1-460c-98cc-45d59e08672d" width="45%" />
</p>

**Widget Utama**

Scaffold, AppBar, Column, ElevatedButton

**Fitur Navigasi**

Home screen menampilkan tombol untuk membuka `DetailScreen`

```
dart
ElevatedButton(
  onPressed: () {
    Navigator.pushNamed(context, '/detail?id=123');
  },
  child: const Text('Go to Detail via Deep Link'),
)
```

**2. DetailScreen**

<p align="center">
  <img src="https://github.com/user-attachments/assets/87070988-74f1-4080-b96d-ca4607537e32" width="45%" />
</p>

**Widget Utama**

Scaffold, AppBar, Text

**Fitur Navigasi**

Menampilkan detail item berdasarkan ID yang dipilih atau dari URI. Terdapat tombol untuk kembali ke halaman utama.

### Modifikasi Kode
Dilakukan penambahan route settingg seperti gambar berikut:

<p align="center">
  <img src="https://github.com/user-attachments/assets/df8d339b-99db-42a7-9c24-cb16b4cef143" width="45%" />
  <img src="https://github.com/user-attachments/assets/0225b0a4-2eb9-4273-8d6f-f38044f44d8c" width="45%" />
</p>

- Layar setting
```
// Layar Settings (SettingsScreen)
class SettingsScreen extends StatelessWidget {
  const SettingsScreen({super.key});

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(title: const Text('Settings'), centerTitle: true),
      body: const Center(
        child: Text(
          'Halaman Settings',
          style: TextStyle(fontSize: 20),
        ),
      ),
    );
  }
}
```

- Penambahan icon setting pada appbar
```
      appBar: AppBar(
        title: const Text('Home'),
        centerTitle: true,
        actions: [
          IconButton(
            icon: const Icon(Icons.settings),
            onPressed: onSettingsSelected,
            tooltip: 'Settings',
          ),
        ],
      ),
```

Penambahan variabel 
```
class HomeScreen extends StatelessWidget {
  final List<Item> items;
  final Function(int) onItemSelected;
  final VoidCallback onSettingsSelected;

  const HomeScreen({
    super.key,
    required this.items,
    required this.onItemSelected,
    required this.onSettingsSelected,
  });
```

Penanganan rute setting
```
    if (uri.pathSegments.length == 1 && uri.pathSegments[0] == 'settings') {
      return RoutePath.settings();
    }
```
```
  RouteInformation restoreRouteInformation(RoutePath path) {
    if (path.isHome) {
      return RouteInformation(uri: Uri.parse('/'));
    }
    if (path.isDetail) {
      return RouteInformation(uri: Uri.parse('/detail/${path.id}'));
    }
    if (path.isSettings) {
      return RouteInformation(uri: Uri.parse('/settings'));
    }
    return RouteInformation(uri: Uri.parse('/'));
  }
```

Lalu ada penambahan kelas konfigurasi rute dan perubahan-perubahan kecil lainnya.

