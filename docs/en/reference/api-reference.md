---
title: API Reference
---

# API Reference

REST API endpoints for TAVP CMS.

## Authentication

All API endpoints require a Bearer token:

```bash
curl -H "Authorization: Bearer YOUR_TOKEN" https://yoursite.com/api/cms/types
```

Generate tokens with:

```bash
tavp hub:make:resource ApiToken
# Or manually in config/cms.php
```

## Content Types

| Method | Endpoint | Description |
|--------|----------|-------------|
| GET | `/api/cms/types` | List all content types |

## Records

| Method | Endpoint | Description |
|--------|----------|-------------|
| GET | `/api/cms/{type}` | Browse records (paginated) |
| GET | `/api/cms/{type}/{id}` | Read a single record |
| POST | `/api/cms/{type}` | Create a record |
| PUT | `/api/cms/{type}/{id}` | Update a record |
| DELETE | `/api/cms/{type}/{id}` | Delete a record |

### Query Parameters (Browse)

| Param | Default | Description |
|-------|---------|-------------|
| `page` | 1 | Page number |
| `per_page` | 15 | Items per page (max: 100) |
| `status` | — | Filter by status |

## Search

| Method | Endpoint | Description |
|--------|----------|-------------|
| GET | `/api/cms/search?q={query}` | Full-text search |
| GET | `/api/cms/search?q={query}&type=post` | Search within type |

## Taxonomy

| Method | Endpoint | Description |
|--------|----------|-------------|
| GET | `/api/cms/taxonomy/{type}` | List terms (category, tag) |
| POST | `/api/cms/taxonomy` | Create a term |

## Revisions

| Method | Endpoint | Description |
|--------|----------|-------------|
| GET | `/api/cms/{type}/{id}/revisions` | Revision history |
| POST | `/api/cms/{type}/{id}/rollback/{ts}` | Rollback to revision |

## Sitemap

| Method | Endpoint | Description |
|--------|----------|-------------|
| GET | `/sitemap.xml` | Auto-generated sitemap |

## Response Format

```json
{
    "data": {},
    "meta": {
        "total": 100,
        "per_page": 15,
        "current_page": 1
    }
}
```

## Error Response

```json
{
    "error": "Not found",
    "message": "Record not found"
}
```

## Examples

### Browse Posts

```bash
curl -H "Authorization: Bearer YOUR_TOKEN" \
  "https://yoursite.com/api/cms/post?page=1&per_page=10"
```

### Create Post

```bash
curl -X POST -H "Authorization: Bearer YOUR_TOKEN" \
  -H "Content-Type: application/json" \
  -d '{"title":"Hello","slug":"hello","body":"World","status":"published"}' \
  https://yoursite.com/api/cms/post
```

### Search

```bash
curl -H "Authorization: Bearer YOUR_TOKEN" \
  "https://yoursite.com/api/cms/search?q=hello&type=post"
```

## Link

- [TAVP CMS](/ecosystem/tavp-cms)
- [FAQ](/reference/faq)
