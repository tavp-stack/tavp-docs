# Runtimes

TAVP supports 4 runtime options. All share the same application code — only the runtime changes.

## Overview

| Runtime | Speed | Best For |
|---------|-------|----------|
| PHP-FPM | Standard | Shared hosting, traditional |
| TAVP Coil | Fastest | High traffic, real-time |
| TAVP Relay | Fast | Enterprise, balanced |
| TAVP Weave | Standard | Shared hosting, parallel I/O |

## PHP-FPM (Default)

Traditional PHP runtime. Works everywhere.

- Standard PHP execution
- Works on shared hosting
- No extensions required
- **Best for:** Development, shared hosting

```bash
tavp serve
```

## TAVP Coil (Swoole)

Coroutine-based runtime. Highest performance.

- Native coroutines via Swoole C-extension
- Async I/O: hooks all blocking PHP functions
- Persistent memory: Phalcon booted once per worker
- 10,000+ concurrent coroutines per worker
- Connection pooling (MySQL, Redis, HTTP)
- Built-in: timer, task queue, WebSocket server
- **Requires:** Swoole extension + VPS/dedicated server
- **Risks:** Memory leaks, state pollution, debug difficulty — all mitigated by RequestCleanup mechanism

```bash
tavp coil:start --workers=4
```

## TAVP Relay (RoadRunner)

Go-based application server. Enterprise-grade.

- Go-based server handles HTTP, Queue, WebSocket, gRPC, Metrics
- Process isolation: PHP crash does not take down Go server
- Automatic worker restart on failure
- Built-in job pipeline (no external queue needed)
- Prometheus metrics export
- Single Go binary — no external dependencies
- **Requires:** RoadRunner binary + VPS/dedicated server
- **Inspired by:** Spiral Framework (5-10x faster than Laravel/Symfony)

```bash
tavp relay:start --workers=4
```

## TAVP Weave (PHP Fibers)

Cooperative multitasking built into PHP 8.1+.

- Zero external dependencies (no extensions needed)
- Works on shared hosting (PHP-FPM compatible)
- Parallel I/O: HTTP calls, DB queries in one request
- Synchronous-looking syntax (no callback hell)
- **Limitation:** Cannot hook blocking functions (not true non-blocking)
- **Best for:** Shared hosting, lightweight parallel operations

```php
use Tavp\Coil\Facades\Weave;

$results = Weave::gather([
    fn() => Http::get('https://api.example.com/users'),
    fn() => DB::select('SELECT * FROM posts'),
]);
```

## Coexistence

All runtimes share the same application code. A single project can use TAVP Relay as production server, TAVP Weave for parallel I/O inside controllers, and fall back to PHP-FPM on shared hosting.

**Only the runtime changes. Zero code rewrite required.**

## Links

- [PHP-FPM](/en/runtimes/php-fpm)
