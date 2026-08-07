# Security

Security features untuk TAVP.

## CSRF Protection

```php
// Middleware
\Tavp\Middleware\ValidateCsrfToken::class

// In forms
{{ csrf_field() }}
```

## Password Hashing

```php
// Hash
$hashed = password_hash($password, PASSWORD_BCRYPT);

// Verify
if (password_verify($password, $hashed)) {
    // correct
}
```

## XSS Prevention

```volt
{{ user.name }}
{{ user.content | raw }}
```

## SQL Injection Prevention

```php
// Use parameterized queries
$users = DB::select('SELECT * FROM users WHERE email = ?', [$email]);

// Use ORM (safe by default)
$user = User::where('email', $email)->first();
```

## Rate Limiting

```php
$router->post('/api/auth/login', [
    'middleware' => 'throttle:5,1',
    'uses' => 'AuthController@login',
]);
```

## Security Headers

```php
'X-Content-Type-Options' => 'nosniff',
'X-Frame-Options' => 'DENY',
'X-XSS-Protection' => '1; mode=block',
```

## SOP: Jangan Komit Rahasia

Aturan yang berlaku untuk semua repository TAVP (dan project yang memakainya).

### Larangan

- Token API, password, kunci privat, sertifikat `.pem`/`.key`, file `.env` asli, dan file state alat bantu lokal.
- File dump/seed/backup yang berisi data produksi.

### `.env` dan `.env.example`

- Repo hanya boleh memuat `.env.example` (template dengan placeholder).
- `.gitignore` wajib memuat `.env` dan `.env.*` kecuali `.env.example`.

### Token lintas project

Token API yang dipakai banyak project disimpan **di luar repository**, misalnya di file secret global pada HOME developer (contoh: `~/.tavpbox/secrets.yml`). Dengan begitu project lain bisa membaca token yang sama tanpa risiko ikut ter-push ke git. Pola akses dicatat di setiap SOP lokal masing-masing project.

### Bila secret bocor ke riwayat

1. Segera revoke/nonaktifkan token itu di panel (mis. Gitea → Settings → Applications).
2. Buat token baru.
3. Rewrite riwayat git untuk menghapus file/commit yang menyimpan secret:
   ```bash
   git filter-repo --path <path> --invert-paths --force
   git push --force <remote> <branch>
   ```
4. Verifikasi ulang bahwa token tidak lagi muncul di `git log --all` (atau pakai deteksi pola).
5. Rotasi nilai di semua config/env yang memakainya.

### Checklist sebelum commit

- `.env` tidak ikut (hanya `.env.example`).
- Tidak ada nilai secret literal di kode/berkas yang di-commit.
- Folder state alat bantu lokal di-ignore.
- Tidak ada `.pem`/`.key`/`id_*`/`credentials`/`*.p12`.
- Tidak ada dump/backup data produksi.

## Link

- [Reference](/reference/cli-commands)
- [Contributing](/community/contributing)
