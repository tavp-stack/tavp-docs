---
title: Todo Example
---

# Todo Example

A simple task management app.

## Features

- Create, complete, delete tasks
- Filter by status (all, active, completed)
- Simple REST API

## Quick Start

```bash
tavp new my-todo
cd my-todo
tavp migrate
tavp serve
```

## Routes

```php
$router->get('/', [TodoController::class, 'index']);
$router->post('/todos', [TodoController::class, 'store']);
$router->post('/todos/{id}/complete', [TodoController::class, 'complete']);
$router->post('/todos/{id}/delete', [TodoController::class, 'destroy']);
```

## Model

```php
class Todo extends Model
{
    protected string $table = 'todos';
    protected array $fillable = ['title', 'completed'];
    protected array $casts = ['completed' => 'boolean'];
}
```

## Controller

```php
class TodoController extends BaseController
{
    public function index(): string
    {
        $todos = $this->db->query('SELECT * FROM todos ORDER BY created_at DESC');
        return $this->view('todos/index', ['todos' => $todos]);
    }

    public function store(): Response
    {
        $title = $this->request->input('title');
        $this->db->insert('todos', ['title' => $title, 'completed' => false]);
        return $this->redirect('/');
    }
}
```

## Learn More

- [Quick Start](/guide/quick-start)
- [ORM](/features/orm)
