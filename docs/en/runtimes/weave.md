# TAVP Weave

PHP Fibers-based runtime for TAVP.

## What is Weave?

TAVP Weave is cooperative multitasking built into PHP 8.1+. Zero external dependencies, works on shared hosting.

## Usage

```php
use Tavp\Coil\Facades\Weave;

// Parallel HTTP calls
$results = Weave::gather([
    fn() => Http::get('https://api.example.com/users'),
    fn() => Http::get('https://api.example.com/posts'),
    fn() => Http::get('https://api.example.com/comments'),
]);

// Parallel DB queries
$results = Weave::gather([
    fn() => User::all(),
    fn() => Post::all(),
    fn() => Comment::all(),
]);
```

## Features

- Zero external dependencies (no extensions needed)
- Works on shared hosting (PHP-FPM compatible)
- Parallel I/O: HTTP calls, DB queries in one request
- Synchronous-looking syntax (no callback hell)

## Limitations

- Cannot hook blocking functions (not true non-blocking)
- Best for shared hosting, lightweight parallel operations

## Comparison

| Feature | Weave | Coil | Relay |
|---------|-------|------|-------|
| Extension required | No | Swoole | RoadRunner |
| Shared hosting | Yes | No | No |
| True async | No | Yes | Yes |
| Concurrency | Limited | 10K+ coroutines | Workers |

## Links

- [Performance](/en/reference/performance)
