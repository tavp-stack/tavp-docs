---
title: Tavp Starter
---

# Tavp Starter

Project template with a working demo app. Clone and build.

## Quick Start

```bash
composer create-project tavp/starter my-app
cd my-app
cp .env.example .env
tavp phalcon:install
tavp migrate
tavp serve
```

Open http://localhost:8000

## Demo App: Fleet Log

The starter includes a **Vehicle Logbook** demo that showcases TAVP conventions:

- **Dashboard** — stats (vehicles, fuel cost, maintenance cost)
- **Vehicles** — CRUD (motorcycle, car, truck, van, bus)
- **Fuel Tracking** — log entries (odometer, liters, price, station)
- **Maintenance** — log service records with cost

## What It Demonstrates

### Models (PascalCase, snake_case table)

```php
class Vehicle extends Model
{
    protected string $table = 'vehicles';
    protected array $fillable = ['name', 'type', 'brand', 'model', 'year'];
}
```

### Controllers (Controller suffix, snake_case methods)

```php
class VehicleController extends BaseController
{
    public function index(): string { ... }
    public function create(): string { ... }
    public function store(): Response { ... }
    public function edit(string $id): string { ... }
    public function update(string $id): Response { ... }
    public function destroy(string $id): Response { ... }
}
```

### Routes (resource routes)

```php
$router->get('/vehicles', [VehicleController::class, 'index']);
$router->get('/vehicles/create', [VehicleController::class, 'create']);
$router->post('/vehicles', [VehicleController::class, 'store']);
$router->get('/vehicles/{id}/edit', [VehicleController::class, 'edit']);
$router->post('/vehicles/{id}', [VehicleController::class, 'update']);
$router->post('/vehicles/{id}/delete', [VehicleController::class, 'destroy']);
```

### Volt Templates (dark theme)

```volt
{% extends 'layouts/app.volt' %}

{% block content %}
<h1>Vehicles</h1>
{% for v in vehicles %}
    <div>{{ v['name'] }} — {{ v['type'] }}</div>
{% endfor %}
{% endblock %}
```

## Structure

```
app/
  Controllers/         # DashboardController, VehicleController, FuelController
  Models/              # Vehicle, FuelEntry, Maintenance
config/                # app.php, database.php
database/migrations/   # 001_create_tables.php
resources/views/       # Volt templates (dark theme)
routes/web.php         # Resource routes
```

## Conventions

See [CONVENTIONS.md](https://github.com/tavp-stack/tavp-core/blob/main/CONVENTIONS.md) for the full coding standards.

| Element | Convention | Example |
|---------|-----------|---------|
| Classes | PascalCase | `VehicleController` |
| Functions | snake_case, verb+noun | `get_all_vehicles()` |
| Variables | snake_case, full words | `$vehicle_name` |
| Tables | plural snake_case | `vehicles`, `fuel_entries` |
| Routes | descriptive params | `/vehicles/{id}/fuel` |

## Requirements

- PHP 8.3+
- Phalcon 5.16+ (install with `tavp phalcon:install`)

## Learn More

- [Architecture](/architecture/overview)
- [Coding Standards](/standards/overview)
- [GitHub](https://github.com/tavp-stack/tavp-starter)
