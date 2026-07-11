---
title: Storage
---

# Storage

TAVP supports multiple storage drivers: database, flat-file, and cache.

## Storage Drivers

| Driver | Use Case | Data Format |
|--------|----------|-------------|
| **Database** | Production apps | MySQL/PostgreSQL/SQLite |
| **Flat-file** | Blogs, documentation | Markdown + YAML front matter |
| **Cache** | Performance | File-based or APCu |

## Database Storage

```php
// config/database.php
return [
    'default' => 'mysql',
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

## Flat-file Storage (Statamic-style)

Content stored as Markdown + YAML front matter:

```markdown
---
title: Hello World
status: published
created_at: 2026-07-11
---

This is the body content in **Markdown**.
```

### Directory Structure

```
content/
  page/
    about.md
    contact.md
  post/
    hello-world.md
    second-post.md
```

### Config

```php
// config/cms.php
'storage' => 'flatfile',
'drivers' => [
    'flatfile' => [
        'path' => base_path('content'),
        'format' => 'markdown',
    ],
],
```

## Cache Storage

```php
// Wrap any storage with cache
$store = new CachedContentStore(
    inner: $databaseStore,
    cachePath: storage_path('cms/cache'),
    ttl: 300, // 5 minutes
);
```

## API Usage

```php
// Browse records
$records = $bread->browse('post', ['status' => 'published']);

// Read single record
$post = $bread->read('post', 'hello-world');

// Create record
$bread->add('post', ['title' => 'Hello', 'body' => 'World']);

// Update record
$bread->edit('post', 'hello-world', ['title' => 'Updated']);

// Delete record
$bread->delete('post', 'hello-world');
```

## Learn More

- [BREAD CRUD](/features/cms)
- [Flat-file format](https://jekyllrb.com/docs/front-matter/)
