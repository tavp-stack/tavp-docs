---
title: TavpHub
---

# TavpHub — Admin Panel Module

Auto-generated admin panel with controllers, views, and CRUD routing.

## Installation

```bash
composer require tavp/tavphub
```

## Quick Start

### 1. Define Resources

```php
// config/hub.php
return [
    'admin_prefix' => '/admin',
    'brand' => 'My App',
    'resources' => [
        'post' => [
            'label' => 'Posts',
            'singular' => 'Post',
            'model' => \App\Models\Post::class,
            'columns' => [
                ['field' => 'title', 'label' => 'Title'],
                ['field' => 'status', 'label' => 'Status'],
                ['field' => 'created_at', 'label' => 'Created'],
            ],
            'fields' => [
                ['name' => 'title', 'type' => 'text', 'required' => true],
                ['name' => 'slug', 'type' => 'slug'],
                ['name' => 'body', 'type' => 'textarea'],
                ['name' => 'status', 'type' => 'select', 'options' => ['draft', 'published']],
            ],
        ],
    ],
];
```

### 2. Register Routes

```php
// routes/web.php
\Tavp\Hub\HubModule::routes($router);
```

### 3. Done!

Visit `/admin` — you get:
- Login (OTP via tavpid)
- Dashboard with stats
- Resource CRUD (index/create/edit/delete)

## Controllers

| Controller | Purpose |
|-----------|---------|
| `HubController` | Base class (auth guard, sidebar, flash) |
| `DashboardController` | Stats overview |
| `ResourceController` | Generic BREAD CRUD |
| `AuthController` | Login/logout via tavpid |

## Resource Definition

```php
'resources' => [
    'post' => [
        'label' => 'Posts',           // sidebar label
        'singular' => 'Post',          // singular form
        'model' => Post::class,        // model class
        'icon' => 'document',          // sidebar icon
        'columns' => [...],            // table columns
        'fields' => [...],             // form fields
    ],
]
```

### Field Types

| Type | Description |
|------|-------------|
| `text` | Text input |
| `textarea` | Multi-line text |
| `richtext` | Rich text editor |
| `select` | Dropdown |
| `toggle` | Boolean toggle |
| `date` | Date picker |
| `datetime` | DateTime picker |
| `number` | Number input |
| `email` | Email input |
| `slug` | URL slug |
| `file` | File upload |

## HubModule Routes

```
GET  /admin                    → Dashboard
GET  /admin/login              → Login form
POST /admin/login              → Send OTP
GET  /admin/verify             → Verify form
POST /admin/verify             → Verify OTP
POST /admin/logout             → Logout

GET  /admin/resource/{type}           → List records
GET  /admin/resource/{type}/create    → Create form
POST /admin/resource/{type}           → Store record
GET  /admin/resource/{type}/{id}/edit → Edit form
POST /admin/resource/{type}/{id}      → Update record
POST /admin/resource/{type}/{id}/delete → Delete record
```

## Customization

### Custom Admin Theme

Publish views to your project:

```
resources/views/hub/
  layouts/admin.volt
  auth/login.volt
  auth/verify.volt
  dashboard.volt
  resource/index.volt
  resource/form.volt
```

### Custom Controller

Extend `HubController` for custom admin pages:

```php
class ReportController extends HubController
{
    public function index(): string
    {
        if ($r = $this->guard()) {
            return $r;
        }

        return $this->view('hub::reports.index', [
            'data' => $this->getReportData(),
        ]);
    }
}
```
