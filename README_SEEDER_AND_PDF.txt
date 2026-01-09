# Tambahan: Seeder, Dummy Data, Role & Export PDF

## Install paket PDF
```
composer require barryvdh/laravel-dompdf
php artisan vendor:publish --provider="Barryvdh\DomPDF\ServiceProvider"
```

## Jalankan seeder penuh
```
php artisan migrate:fresh --seed
```
Seeder membuat:
- Role (admin/cashier/manager) + 3 user:
  - admin@bakmi.test / password
  - kasir@bakmi.test / password
  - manager@bakmi.test / password
- 6 meja
- menu contoh
- item stok basah & kering
- dummy:
  - transaksi 30 hari terakhir (otomatis dengan item)
  - belanja basah harian acak
  - belanja kering awal bulan + pengambilan acak

## Export PDF Laporan Harian
- Route: `GET /reports/daily/{date}/pdf` — contoh: `/reports/daily/2025-08-26/pdf`
- Tombol PDF bisa kamu tambahkan di halaman laporan harian atau pakai URL di atas.

## Merge route tambahan
Gabungkan `routes_web_extra.php` ke `routes/web.php` Anda untuk endpoint PDF.
