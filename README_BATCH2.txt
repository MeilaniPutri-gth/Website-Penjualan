# Batch 2 — Stock Logs & Admin Corrections

Copy files ke project Laravel kamu dan gabungkan `routes/web_stock_logs_snippet.php` ke `routes/web.php`.
Pastikan alias middleware `role` sudah ditambahkan di `bootstrap/app.php`.

- Controller:
  app/Http/Controllers/StockLogController.php

- Views:
  resources/views/stock/wet_logs.blade.php
  resources/views/stock/dry_logs.blade.php
  resources/views/stock/_edit_wet_purchase.blade.php
  resources/views/stock/_edit_dry_usage.blade.php

- Routes snippet:
  routes/web_stock_logs_snippet.php

Akses:
- /stock/wet/logs?month=YYYY-MM
- /stock/dry/logs?month=YYYY-MM

Edit/Hapus hanya admin.
