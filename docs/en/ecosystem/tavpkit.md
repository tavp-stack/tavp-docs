---
title: TavpKit
---

# TavpKit — Starter Kits

Pre-built starter kits for common project types.

## Available Kits

| Kit | Description | Modules |
|-----|-------------|---------|
| `blog` | Blog with posts, categories, tags | tavp-cms |
| `saas` | SaaS starter with auth, billing, teams | tavp-cms, tavpid, tavphive |
| `ecommerce` | E-commerce with products and orders | tavp-cms |

## Install a Kit

```bash
tavp kit:install blog
tavp kit:install saas
tavp kit:install ecommerce
```

## What Gets Installed

### Blog Kit

- `tavp-cms` — content management
- Content types: `post`, `page`
- Blog routes (`/blog`, `/blog/{slug}`)
- Category + tag taxonomy

### SaaS Kit

- `tavp-cms` — content management
- `tavp/tavpid` — OTP authentication
- `tavp/tavphive` — billing (Stripe, Midtrans)
- User teams + API tokens

### E-commerce Kit

- `tavp-cms` — content management
- Content types: `product`, `order`, `page`
- Product catalog routes

## Custom Kits

Create your own kit by defining a kit class:

```php
use Tavp\Kit\StarterKit;

class MyKit extends StarterKit
{
    public function name(): string
    {
        return 'my-kit';
    }

    public function modules(): array
    {
        return ['tavp-cms', 'tavpid'];
    }

    public function migrations(): array
    {
        return ['create_products_table'];
    }
}
```

## Link

- [TAVP CMS](/ecosystem/tavp-cms)
- [GitHub](https://github.com/tavp-stack/tavpkit)
