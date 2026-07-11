---
title: BREAD Manager
---

# BREAD Manager

Core CRUD engine for TAVP CMS. BREAD = **Browse, Read, Edit, Add, Delete**.

## What It Does

BreadManager provides generic CRUD operations for any content type. Define a content type with fields, and BreadManager handles all database operations automatically.

```php
use Tavp\Cms\Bread\BreadManager;

// Get from container
$bread = app()->getService(BreadManager::class);

// Browse (list) records
$posts = $bread->browse('post', ['status' => 'published']);

// Read a single record
$post = $bread->read('post', 'hello-world');

// Add (create) a record
$newPost = $bread->add('post', [
    'title' => 'Hello World',
    'slug' => 'hello-world',
    'body' => 'This is my first post.',
    'status' => 'published',
]);

// Edit (update) a record
$bread->edit('post', 'hello-world', [
    'title' => 'Updated Title',
]);

// Delete a record
$bread->delete('post', 'hello-world');
```

## Content Types

Define content types in `config/cms.php`:

```php
'content_types' => [
    'post' => [
        'label' => 'Posts',
        'singular' => 'Post',
        'icon' => 'newspaper',
        'route' => '/blog/{slug}',
        'fields' => [
            ['name' => 'title', 'type' => 'text', 'required' => true],
            ['name' => 'slug', 'type' => 'slug', 'from' => 'title'],
            ['name' => 'body', 'type' => 'richtext'],
            ['name' => 'status', 'type' => 'select', 'options' => ['draft', 'published']],
        ],
    ],
],
```

## Field Types

| Type | Description |
|------|-------------|
| `text` | Text input |
| `textarea` | Multi-line text |
| `richtext` | Rich text editor |
| `slug` | URL slug (auto-generated from source) |
| `number` | Number input |
| `boolean` | Toggle/checkbox |
| `select` | Dropdown select |
| `date` | Date picker |
| `datetime` | DateTime picker |
| `media` | File upload |
| `relation` | Related content |
| `blocks` | Block editor |
| `json` | Raw JSON |

## Validation

```php
'fields' => [
    ['name' => 'title', 'type' => 'text', 'required' => true, 'rules' => ['max:200']],
    ['name' => 'email', 'type' => 'text', 'rules' => ['email', 'unique']],
    ['name' => 'price', 'type' => 'number', 'rules' => ['numeric', 'min:0']],
],
```

## Storage Drivers

BreadManager works with any storage driver:

| Driver | Use Case |
|--------|----------|
| `DatabaseStore` | MySQL/PostgreSQL/SQLite |
| `FlatFileStore` | Markdown + YAML (Statamic-style) |

```php
// Config
'storage' => 'flatfile',  // or 'database'

// Same API regardless of driver
$posts = $bread->browse('post');
$post = $bread->read('post', 'hello-world');
```

## Revisions

BreadManager automatically snapshots changes when revisions are enabled:

```php
// config/cms.php
'revisions' => ['enabled' => true, 'limit' => 50],

// View revision history
$history = $bread->history('post', 'hello-world');

// Rollback to a specific revision
$bread->restore('post', 'hello-world', $snapshotData);
```

## Search

```php
$search = app()->getService(SearchEngine::class);
$results = $search->search('hello', 'post', 20);
```

## Learn More

- [TAVP CMS](/ecosystem/tavp-cms)
- [Features](/features/cms)
- [Configuration](/reference/configuration)
