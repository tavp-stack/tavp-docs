---
title: SaaS Starter Example
---

# SaaS Starter Example

A SaaS application with billing, teams, and multi-tenancy.

## Features

- User authentication (tavpid)
- Team management (tavpkit)
- Subscription billing (tavphive)
- Admin panel (tavphub)
- Multi-tenant data isolation

## Quick Start

```bash
tavp new my-saas
cd my-saas
tavp migrate
tavp serve
```

## Modules Used

| Module | Purpose |
|--------|---------|
| tavpid | OTP login, JWT API auth |
| tavpkit | Team management, API tokens |
| tavphive | Stripe/Midtrans billing |
| tavphub | Admin panel |
| tavp-cms | Content management |

## Routes

```php
// Auth
$router->post('/login', [AuthController::class, 'login']);
$router->post('/register', [AuthController::class, 'register']);

// Teams
$router->get('/teams', [TeamController::class, 'index']);
$router->post('/teams', [TeamController::class, 'store']);

// Billing
$router->get('/billing', [BillingController::class, 'index']);
$router->post('/checkout', [CheckoutController::class, 'store']);
```

## Config

```php
// config/hive.php
return [
    'gateways' => [
        'stripe' => ['driver' => 'stripe', 'secret' => env('STRIPE_SECRET')],
    ],
];
```

## Learn More

- [Architecture](/architecture/overview)
- [Tavpid](/ecosystem/tavpid)
- [TavpKit](/ecosystem/tavpkit)
- [TavpHive](/ecosystem/tavphive)
