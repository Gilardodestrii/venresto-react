# Venresto React

Venresto React adalah versi baru Venresto dengan konsep **Laravel + React dalam satu project**.

Repo lama `Gilardodestrii/venresto` hanya digunakan sebagai referensi dan tidak disentuh.

## Konsep

Laravel tetap menjadi backend utama untuk:

- Routing backend
- Authentication
- API
- Database MySQL
- Business logic POS
- QR Menu
- Inventory
- Kitchen Display
- Reports
- Tenant slug routing seperti repo lama

React berada di dalam Laravel pada folder `resources/js` dan dirender melalui Blade `resources/views/app.blade.php`.

```text
Browser
  -> Laravel route dengan tenant slug
  -> resources/views/app.blade.php
  -> React app di resources/js
  -> API Laravel
  -> MySQL
```

## Struktur React

```text
resources/js/
├── main.jsx
├── App.jsx
├── bootstrap.js
├── components/
│   ├── AppLayout.jsx
│   └── Sidebar.jsx
└── pages/
    ├── Landing.jsx
    ├── Login.jsx
    ├── Dashboard.jsx
    ├── Pos.jsx
    ├── Inventory.jsx
    ├── Kitchen.jsx
    ├── Reports.jsx
    └── Settings.jsx
```

## URL React dengan Tenant Slug

React admin mengikuti pola route repo lama dengan tenant slug:

```text
/
/login
/signup
/{tenant}/login
/{tenant}/admin/dashboard
/{tenant}/admin/pos
/{tenant}/admin/inventory
/{tenant}/admin/kitchen
/{tenant}/admin/reports
/{tenant}/admin/settings
/{tenant}/admin/roles
```

QR menu tetap bisa menggunakan pola tenant juga:

```text
/{tenant}/qr/{table}
```

Laravel tetap menyediakan route API dengan prefix tenant jika diperlukan:

```text
/api/{tenant}/...
```

Jika ada route khusus backend seperti webhook Midtrans, QR download, atau aksi submit form, route tersebut tetap didefinisikan di Laravel dan tidak perlu masuk React Router.

## Contoh Catch-all Route Laravel untuk React Admin

```php
Route::middleware(['auth'])->group(function () {
    Route::get('/{tenant}/admin/{any?}', function (string $tenant) {
        return view('app', [
            'tenant' => $tenant,
        ]);
    })->where('any', '.*')->name('tenant.admin.react');
});
```

## Install Lokal

```bash
composer install
npm install
cp .env.example .env
php artisan key:generate
php artisan migrate
npm run dev
php artisan serve
```

## Build Production

```bash
npm run build
php artisan optimize
```

## Catatan

Repo ini disiapkan sebagai fondasi awal Laravel + React dengan route tenant slug seperti repo lama. Fitur dari repo lama bisa dipindahkan bertahap ke API Laravel dan halaman React.