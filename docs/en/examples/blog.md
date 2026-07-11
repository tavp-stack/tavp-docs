---
title: Blog Example
---

# Blog Example

A complete blog with posts, categories, tags, and SEO.

## Features

- **Posts** — create, edit, delete posts with rich text
- **Categories** — organize posts by category
- **Tags** — tag posts for filtering
- **SEO** — per-post meta titles and descriptions
- **Sitemap** — auto-generated sitemap.xml

## Quick Start

```bash
tavp new my-blog
cd my-blog
tavp migrate
tavp serve
```

## Project Structure

```
app/
  Controllers/
    PostController.php
    CategoryController.php
  Models/
    Post.php
    Category.php
    Tag.php
config/
  cms.php
database/
  migrations/
resources/views/
  posts/
    index.volt
    show.volt
routes/
  web.php
```

## Routes

```php
$router->get('/blog', [PostController::class, 'index']);
$router->get('/blog/{slug}', [PostController::class, 'show']);
$router->get('/category/{slug}', [CategoryController::class, 'show']);
$router->get('/tag/{slug}', [TagController::class, 'show']);
```

## Model

```php
class Post extends Model
{
    protected string $table = 'posts';
    protected array $fillable = ['title', 'slug', 'body', 'status', 'category_id'];
    protected array $casts = ['published_at' => 'datetime'];
}
```

## Controller

```php
class PostController extends BaseController
{
    public function index(): string
    {
        $posts = $this->db->query('SELECT * FROM posts WHERE status = ? ORDER BY created_at DESC', ['published']);
        return $this->view('posts/index', ['posts' => $posts]);
    }

    public function show(string $slug): string
    {
        $post = $this->db->query('SELECT * FROM posts WHERE slug = ?', [$slug])[0] ?? null;
        if (!$post) return response('404', 404);
        return $this->view('posts/show', ['post' => $post]);
    }
}
```

## Learn More

- [ORM](/features/orm)
- [Routing](/features/routing)
- [Views](/features/views)
