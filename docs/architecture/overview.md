---
title: Architecture
---

# Architecture

TAVP is a **modular stack** — independent modules compose into products.

## Module Dependency Graph

```
tavp-core (foundation)
    │
    ├── tavpid (auth: OTP, JWT, session, RBAC)
    ├── tavphub (admin panel: controllers, views, CRUD)
    ├── tavpkit (teams, API tokens, starter kits)
    ├── tavphive (billing: Stripe, Midtrans, PayPal, Xendit)
    ├── tavp-analytics (tracking, fraud detection, experiments)
    ├── tavpblocks (UI components)
    │
    └────→ tavp-cms (composed product: thin glue layer)
```

## How Modules Compose

**tavp-cms** is NOT a monolith. It's a thin glue layer that wires modules together:

```php
// CmsServiceProvider — the entire CMS registration
$app->bind(ContentStore::class, fn () => $this->makeStore());      // storage driver
$app->bind(BreadManager::class, fn () => new BreadManager(...));   // BREAD CRUD
$app->bind(TaxonomyManager::class, fn () => ...);                 // categories + tags
$app->bind(RevisionStore::class, fn () => ...);                   // version history
$app->bind(SearchEngine::class, fn () => ...);                    // full-text search
$app->bind(ThemeManager::class, fn () => ...);                    // Volt themes

// Auth comes from tavpid (not cms)
$app->bind(SessionAuth::class, fn () => new SessionAuth(...));

// Admin comes from tavphub (not cms)
HubModule::routes($router);

// Analytics comes from tavp-analytics (optional)
if (config('cms.analytics.enabled')) {
    AnalyticsManager::register($router);
}
```

## Request Flow

```
HTTP Request
    │
    ▼
public/index.php (entry point)
    │
    ▼
Application::bootstrap() (load config, register services)
    │
    ▼
Router::match() (find matching route)
    │
    ▼
Kernel::handle() (run middleware → dispatch → respond)
    │
    ▼
Controller::method() (business logic)
    │
    ▼
view() or response() (render template or return JSON)
    │
    ▼
HTTP Response
```

## Auth Flow (tavpid)

```
1. User visits /admin/login
2. Enters email → POST /admin/login
3. SessionAuth::requestCode() → generates OTP, stores hash in session
4. Email sent via MailService (SMTP/Mailpit)
5. User enters code → POST /admin/verify
6. SessionAuth::verify() → compares code against hash
7. On success → sets $_SESSION['tavpid_user_id']
8. Redirect to /admin (dashboard)
```

## Admin Flow (tavphub)

```
1. HubModule::routes() registers admin routes
2. DashboardController::index() → shows stats from resources
3. ResourceController::index() → lists records using FormBuilder
4. ResourceController::create() → shows form using FormBuilder
5. ResourceController::store() → saves via model
6. ResourceController::edit() → shows pre-filled form
7. ResourceController::update() → updates via model
8. ResourceController::destroy() → deletes via model
```

## Design Principles

1. **Modules are independent** — each can be used without the others
2. **Products compose modules** — cms, marketplace, saas are thin glue layers
3. **No duplication** — auth lives in tavpid, admin in tavphub, billing in tavphive
4. **Config over code** — features enabled/disabled via config arrays
5. **Storage agnostic** — database or flat-file, same API
