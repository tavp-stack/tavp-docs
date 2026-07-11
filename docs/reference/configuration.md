---
title: Configuration
---

# Configuration

TAVP configuration reference.

## Environment Variables

```env
APP_NAME=TAVP
APP_ENV=local
APP_KEY=base64:...
APP_DEBUG=true
APP_URL=http://localhost:8000

DB_HOST=127.0.0.1
DB_PORT=3306
DB_DATABASE=tavp
DB_USERNAME=root
DB_PASSWORD=secret

MAIL_DRIVER=smtp
MAIL_HOST=mailpit
MAIL_PORT=1025
```

## Config Files

### config/app.php

```php
return [
    'name' => env('APP_NAME', 'TAVP'),
    'env' => env('APP_ENV', 'production'),
    'debug' => (bool) env('APP_DEBUG', false),
    'url' => env('APP_URL', 'http://localhost:8000'),
    'timezone' => 'UTC',
];
```

### config/database.php

```php
return [
    'default' => env('DB_CONNECTION', 'mysql'),
    'connections' => [
        'mysql' => [
            'host' => env('DB_HOST', '127.0.0.1'),
            'port' => (int) env('DB_PORT', 3306),
            'database' => env('DB_DATABASE', 'tavp'),
            'username' => env('DB_USERNAME', 'root'),
            'password' => env('DB_PASSWORD', ''),
        ],
    ],
];
```

### config/cms.php

| Key | Default | Description |
|-----|---------|-------------|
| `storage` | `database` | Storage driver: `database` or `flatfile` |
| `admin.emails` | `[]` | Allowed admin emails for OTP login |
| `admin.brand` | `TAVP CMS` | Admin panel brand name |
| `admin.otp_ttl_minutes` | `10` | OTP expiry time |
| `taxonomy.enabled` | `true` | Enable categories + tags |
| `revisions.enabled` | `true` | Enable version history |
| `search.enabled` | `true` | Enable full-text search |
| `api.enabled` | `true` | Enable headless REST API |
| `analytics.enabled` | `false` | Enable analytics (requires tavp-analytics) |
| `cache.enabled` | `true` | Enable read-through cache |
| `seo.enabled` | `true` | Enable sitemap |
| `webhooks.enabled` | `false` | Enable webhook dispatch |
| `publishing.enabled` | `false` | Enable scheduled publishing |

### config/hub.php

```php
return [
    'admin_prefix' => '/admin',
    'brand' => env('APP_NAME', 'My App'),
    'resources' => [
        // 'post' => [\App\Resources\PostResource::class],
    ],
];
```

### config/hive.php

```php
return [
    'gateways' => [
        'stripe' => [
            'driver' => 'stripe',
            'secret' => env('STRIPE_SECRET', ''),
        ],
        'midtrans' => [
            'driver' => 'midtrans',
            'server_key' => env('MIDTRANS_SERVER_KEY', ''),
        ],
    ],
];
```

## CLI Commands for Config

```bash
tavp env:list          # Show current config
tavp env:switch local  # Switch to local environment
tavp key:generate      # Generate APP_KEY + JWT_SECRET
```

## Link

- [Helpers](/reference/helpers)
- [CLI Commands](/reference/cli-commands)
