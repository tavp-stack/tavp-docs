---
title: TAVP CMS
---

# TAVP CMS

Content management system built on TAVP modules. Thin glue layer — not a monolith.

## What It Is

tavp-cms composes existing modules into a working CMS:

| Concern | Module |
|---------|--------|
| Auth (OTP, session) | tavpid |
| Admin panel | tavphub |
| BREAD CRUD | tavp-core (BreadManager) |
| Storage | tavp-core (DatabaseStore / FlatFileStore) |
| Taxonomy | tavp-core (TaxonomyManager) |
| Revisions | tavp-core (RevisionStore) |
| Search | tavp-core (SearchEngine) |
| Analytics | tavp-analytics (optional) |

## Quick Start

```bash
composer create-project tavp/cms my-site
cd my-site
tavp migrate
tavp serve
```

## Features

- **Pluggable Storage** — Database or flat-file (Markdown + YAML)
- **BREAD Content Types** — auto-generated admin UI
- **OTP Admin Login** — passwordless via tavpid
- **Taxonomy** — categories + tags
- **Revisions** — version history, one-click rollback
- **Search** — full-text across all content types
- **Headless API** — REST with bearer token auth
- **SEO Sitemap** — auto-generated `/sitemap.xml`
- **Analytics** — page view tracking (via tavp-analytics)
- **Dark Admin UI** — modern Tailwind theme

## Configuration

```php
// config/cms.php
return [
    'storage' => 'flatfile',  // or 'database'
    'admin' => [
        'emails' => ['admin@example.com'],
    ],
    'analytics' => [
        'enabled' => true,  // requires tavp-analytics
    ],
];
```

## Content Types

Define in config:

```php
'content_types' => [
    'page' => [
        'label' => 'Pages',
        'fields' => [
            ['name' => 'title', 'type' => 'text', 'required' => true],
            ['name' => 'slug', 'type' => 'slug', 'from' => 'title'],
            ['name' => 'body', 'type' => 'richtext'],
            ['name' => 'status', 'type' => 'select', 'options' => ['draft', 'published']],
        ],
    ],
],
```

## API Endpoints

| Method | Endpoint | Description |
|--------|----------|-------------|
| GET | `/api/cms/types` | List content types |
| GET | `/api/cms/{type}` | Browse records |
| GET | `/api/cms/{type}/{id}` | Read record |
| POST | `/api/cms/{type}` | Create record |
| PUT | `/api/cms/{type}/{id}` | Update record |
| DELETE | `/api/cms/{type}/{id}` | Delete record |
| GET | `/api/cms/search?q=...` | Full-text search |
| GET | `/sitemap.xml` | Auto-generated sitemap |

## Architecture

tavp-cms is a **thin glue layer** — no auth code, no admin code, no RBAC code of its own. Everything comes from modules.

See [Architecture Overview](/architecture/overview) for details.
