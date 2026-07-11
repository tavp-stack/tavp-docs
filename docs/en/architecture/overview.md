---
title: Architecture
---

# Architecture

TAVP is a **modular stack** — independent modules compose into products.

## Module Dependency Graph

```
tavp-core (foundation: routing, ORM, Volt, queue, DB)
    │
    ├── tavpid (auth: OTP, JWT, session, RBAC)
    ├── tavphub (admin panel: controllers, views, CRUD)
    ├── tavpkit (teams, API tokens, starter kits)
    ├── tavphive (billing: Stripe, Midtrans, PayPal, Xendit)
    ├── tavp-analytics (tracking, fraud detection, experiments)
    ├── tavpblocks (20 UI components)
    │
    └────→ tavp-cms (composed product: thin glue layer)
              │
              ├── DashboardController (stats)
              ├── ContentController (BREAD CRUD)
              ├── TeamController (from tavpkit)
              ├── BillingController (from tavphive)
              ├── MediaController (file upload)
              ├── MenuController (nestable menus)
              ├── SettingsController (key/value)
              ├── AnalyticsController (from tavp-analytics)
              ├── RevisionController (version history)
              ├── SearchController (full-text search)
              └── TaxonomyController (categories + tags)
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
$app->bind('tavpid.auth', fn () => new AuthService(...));
$app->bind('tavpid.session', fn () => new SessionAuth(...));
$app->bind('tavpid.rbac', fn () => new AccessControl(...));

// Admin comes from tavphub (not cms)
HubModule::routes($router);

// Teams come from tavpkit (not cms)
// Billing comes from tavphive (not cms)
// Analytics comes from tavp-analytics (optional)
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

## Team Flow (tavpkit)

```
1. TeamController::index() → lists all teams
2. TeamController::create() → shows team form
3. TeamController::store() → creates team with owner
4. TeamController::edit() → shows team + members
5. TeamController::addMember() → adds user to team
6. TeamController::removeMember() → removes user from team
```

## Billing Flow (tavphive)

```
1. BillingController::index() → shows subscriptions + stats
2. BillingController::invoices() → lists all invoices
3. BillingController::cancelSubscription() → cancels a subscription
4. Gateway handles checkout (Stripe/Midtrans/PayPal/Xendit)
```

## Marketplace Flow (tavpmarketplace)

```
1. LocalMarketplace::search() → find modules by name/description
2. LocalMarketplace::get() → get module details
3. LocalMarketplace::publish() → register a module
4. LocalMarketplace::install() → copy module files to project
5. API server: GET/POST /api/modules
```

## Design Principles

1. **Modules are independent** — each can be used without the others
2. **Products compose modules** — cms, marketplace, saas are thin glue layers
3. **No duplication** — auth lives in tavpid, admin in tavphub, billing in tavphive, teams in tavpkit
4. **Config over code** — features enabled/disabled via config arrays
5. **Storage agnostic** — database or flat-file, same API
