---
title: AI Coding Standards
---

# AI Coding Standards

Conventions for generating TAVP code with AI tools.

## Prompt Template

Use this prompt when generating TAVP code:

```
Generate PHP code following TAVP Stack conventions:

- PSR-4 autoloading, snake_case functions/variables, PascalCase classes
- Models extend Tavp\Core\Database\Model with $table, $fillable, $casts
- Controllers extend BaseController, return string|Response
- Use app()->getService() for dependency injection
- Use response('content', 200) or redirect('/path') helpers
- Volt templates use {% extends %} and {% block content %}
- No abbreviations, full English words, descriptive names
- Booleans start with is_, has_, can_, should_
- Functions use verb + noun: get_user_by_email(), create_new_post()
```

## File Naming

| Type | Convention | Example |
|------|-----------|---------|
| PHP class | PSR-4 (class = file name) | `User.php`, `PaymentService.php` |
| Volt template | lowercase, hyphen-separated | `admin-dashboard.volt` |
| Migration | Sequential numbers | `001_create_users_table.php` |
| Config | lowercase | `cms.php`, `database.php` |

## Variable Naming

```php
// GOOD — full English words
$user_email = 'test@example.com';
$post_count = 10;
$is_authenticated = true;
$order_list = [];

// BAD — abbreviations
$email = 'test@example.com';
$cnt = 10;
$auth = true;
$data = [];
```

## Function Naming

```php
// GOOD — verb + noun
get_user_by_email($email)
get_all_published_posts()
create_new_user($data)
update_user_profile($user, $data)
delete_post_by_id($post_id)

// BAD — camelCase or unclear
getUser($email)
fetch()
processData($d)
```

## Class Naming

| Suffix | Purpose | Example |
|--------|---------|---------|
| `Controller` | HTTP handlers | `AuthController` |
| `Service` | Business logic | `PaymentService` |
| (none) | Models | `User`, `Post` |
| `Middleware` | Request filters | `VerifyCsrfToken` |
| `Job` | Queued tasks | `SendWelcomeEmailJob` |
| `Event` | Something happened | `UserRegisteredEvent` |

## Model Convention

```php
<?php
namespace App\Models;

use Tavp\Core\Database\Model;

class Post extends Model
{
    protected string $table = 'posts';
    protected array $fillable = ['title', 'slug', 'body', 'status'];
    protected array $casts = ['published_at' => 'datetime'];
}
```

## Controller Convention

```php
<?php
namespace App\Controllers;

use Tavp\Core\Http\Response;

class PostController extends BaseController
{
    public function index(): string
    {
        $posts = $this->service('post')->get_all_published_posts();
        return $this->view('posts.index', ['posts' => $posts]);
    }

    public function show(string $slug): string|Response
    {
        $post = $this->service('post')->get_post_by_slug($slug);
        if ($post === null) {
            return response('404 Not Found', 404);
        }
        return $this->view('posts.show', ['post' => $post]);
    }
}
```

## Route Convention

```php
// Resource routes
$router->get('/posts', [PostController::class, 'index']);
$router->get('/posts/{slug}', [PostController::class, 'show']);
$router->post('/posts', [PostController::class, 'store']);

// Named routes with closures
$router->get('/about', function () {
    return view('pages.about');
});
```

## Volt Template Convention

```volt
{% extends 'layouts/app.volt' %}

{% block content %}
<h1>{{ post.title }}</h1>
<div class="body">{{ post.body }}</div>

{% if post.categories is defined %}
    {% for category in post.categories %}
        <span class="tag">{{ category.name }}</span>
    {% endfor %}
{% endif %}
{% endblock %}
```

## Error Messages

```php
// GOOD — specific, actionable
'The e-mail address is not valid.'
'Post not found with slug: hello-world'

// BAD — vague
'Invalid input.'
'Error.'
```

## Full Reference

See [CONVENTIONS.md](https://github.com/tavp-stack/tavp-core/blob/main/CONVENTIONS.md) for the complete coding standards.
