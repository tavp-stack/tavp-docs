# Security

Security features for TAVP.

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

## SOP: Never Commit Secrets

Rules that apply to every TAVP repository (and projects built on it).

### Forbidden

- API tokens, passwords, private keys, `.pem`/`.key` certificates, real `.env` files, and local tooling state files.
- Dumps/seeds/backups containing production data.

### `.env` and `.env.example`

- Repositories may only contain `.env.example` (a template with placeholders).
- `.gitignore` must include `.env` and `.env.*` except `.env.example`.

### Cross-project tokens

API tokens shared by several projects live **outside the repository** — for example in a global secrets file in the developer's HOME (e.g. `~/.tavpbox/secrets.yml`). Other projects can read the same token without risking it being pushed to git. The exact access pattern is recorded in each project's local SOP.

### If a secret leaks into history

1. Revoke/deactivate that token immediately in the panel (e.g. Gitea → Settings → Applications).
2. Create a new token.
3. Rewrite git history to remove the file/commit holding the secret:
   ```bash
   git filter-repo --path <path> --invert-paths --force
   git push --force <remote> <branch>
   ```
4. Verify the token no longer appears in `git log --all` (or use pattern detection).
5. Rotate the value in every config/env that uses it.

### Pre-commit checklist

- `.env` is not tracked (only `.env.example`).
- No literal secret values in committed code or files.
- Local tooling state folder is ignored.
- No `.pem`/`.key`/`id_*`/`credentials`/`*.p12`.
- No production dump/backup files.

## Links

- [Reference](/en/reference/cli-commands)
- [Contributing](/en/community/contributing)
