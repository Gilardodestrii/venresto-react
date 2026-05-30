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

React berada di dalam Laravel pada folder `resources/js` dan dirender melalui Blade `resources/views/app.blade.php`.

```text
Browser
  -> Laravel route
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
    ├── Dashboard.jsx
    ├── Pos.jsx
    ├── Inventory.jsx
    ├── Kitchen.jsx
    ├── Reports.jsx
    └── Settings.jsx
```

## URL React

React akan aktif di route:

```text
/app
/app/dashboard
/app/pos
/app/inventory
/app/kitchen
/app/reports
/app/settings
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

Repo ini disiapkan sebagai fondasi awal Laravel + React. Fitur dari repo lama bisa dipindahkan bertahap ke API Laravel dan halaman React.