# Warung Bakmi POS (Laravel + Blade)

Paket ini adalah "drop-in" code untuk Laravel 10+ yang mencakup:
- Fitur Kasir (meja, menu, transaksi, struk).
- Tracking Stock: Bahan Basah (belanja harian) & Bahan Kering (belanja bulanan + pengambilan).
- Closing harian (auto buat laporan berdasarkan transaksi hari itu).
- Dashboard grafik cashflow (Chart.js).
- Request belanja bahan basah -> WhatsApp (tanpa simpan ke database).

## Cara Pakai (ringkas)
1. Buat project baru: `laravel new bakmi` atau `composer create-project laravel/laravel bakmi`
2. Salin seluruh isi folder ini sesuai struktur ke project Laravel Anda (timpa/merge folder `app`, `database`, `resources`, `public`, dan **gabungkan** `routes_web.php` ke `routes/web.php` Anda).
3. Edit `.env` (database dsb). **Opsional:** set nomor WA: `WA_NUMBER=62812xxxxxx`
4. Migrasi: `php artisan migrate`
5. Seed data awal (opsional): insert 6 meja & beberapa menu (lihat snippet di bawah).
6. Jalankan: `php artisan serve` lalu buka `http://localhost:8000/`.

### Merge routes
Buka `routes/web.php` pada project Anda, salin isi `routes_web.php` dari paket ini untuk mengganti/menambahkan rute.

### Seed cepat (Tinker)
```php
php artisan tinker
>>> \App\Models\Meja::insert([
... ['name'=>'Meja 1'],['name'=>'Meja 2'],['name'=>'Meja 3'],
... ['name'=>'Meja 4'],['name'=>'Meja 5'],['name'=>'Meja 6'],
... ]);
>>> \App\Models\Menu::insert([
... ['name'=>'Bakmi Ayam','category'=>'Mie','price'=>15000],
... ['name'=>'Bakmi Goreng','category'=>'Mie','price'=>17000],
... ['name'=>'Pangsit Rebus','category'=>'Side','price'=>8000],
... ['name'=>'Es Teh','category'=>'Minuman','price'=>5000],
... ]);
```
> Catatan: Harga dalam rupiah (integer).

### DomPDF (opsional untuk export PDF "beneran")
Saat ini tombol `Print` menggunakan `window.print()` untuk menyimpan PDF. Jika ingin file PDF server-side:
```
composer require barryvdh/laravel-dompdf
```
Lalu buat route/controller export sesuai kebutuhan.

## Alur Fitur
- **Kasir**: Pilih meja/Takeaway → pilih menu (isi Qty) → konfirmasi (pilih Cash/QRIS) → finalize → cetak struk → kembali ke halaman meja. Meja yang aktif menampilkan tombol *Selesai* untuk mengosongkan status meja.
- **Bahan Basah**: Input belanja harian (qty & total biaya). Ringkasan otomatis per bulan.
- **Bahan Kering**: Input belanja awal bulan → stok bertambah; catat pengambilan → stok berkurang; log per bulan.
- **Closing Harian**: Tekan tombol *Buat Closing Hari Ini* (malam) → sistem rekap transaksi & belanja di hari itu → tampilkan laporan siap cetak.
- **Dashboard**: Chart cash-in vs cash-out untuk harian/mingguan/bulanan/tahunan.
- **Request WA**: Form kebutuhan bahan basah → redirect ke `wa.me` dengan pesan terformat (tanpa simpan DB).

## Struktur Singkat
- Controllers: `CashierController`, `StockController`, `ClosingController`, `DashboardController`, `RequestController`
- Models: `Meja`, `Menu`, `Transaction`, `TransactionItem`, `WetItem`, `WetPurchase`, `DryItem`, `DryPurchase`, `DryUsage`, `Closing`
- Migrations: tabel sesuai model di atas
- Views: Blade siap pakai dengan Bootstrap 5 + Chart.js

### Catatan Teknis
- Validasi dasar sudah ada di setiap form (server-side).
- Tidak ada QR generator; opsi QRIS hanyalah pilihan metode bayar (sesuai permintaan).
- Struk dan laporan harian bisa di-print sebagai PDF lewat dialog browser.
- Script & CSS ringan dan tidak bentrok (Bootstrap via CDN + file lokal `public/css/app.css`, `public/js/app.js`).

Semoga membantu. Selamat membangun sistem Warung Bakmi! 🍜
