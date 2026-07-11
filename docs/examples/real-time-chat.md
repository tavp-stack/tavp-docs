---
title: Real-time Chat Example
---

# Real-time Chat Example

A real-time chat application using WebSockets.

## Features

- Real-time messaging
- Multiple chat rooms
- User presence indicators
- Message history

## Quick Start

```bash
tavp new my-chat
cd my-chat
tavp migrate
tavp serve
```

## Architecture

```
Browser ←→ WebSocket Server ←→ Database
   ↑                              ↑
   └──── TAVP App ────────────────┘
```

## Routes

```php
$router->get('/', [ChatController::class, 'index']);
$router->get('/rooms', [RoomController::class, 'index']);
$router->post('/rooms', [RoomController::class, 'store']);
$router->get('/rooms/{id}', [RoomController::class, 'show']);
```

## WebSocket Server

```php
// Use TAVP Weave for async WebSocket support
$app->bind('websocket', function () {
    return new WebSocketServer([
        'host' => '0.0.0.0',
        'port' => 9501,
    ]);
});
```

## Learn More

- [Coil Runtime](/runtimes/coil)
- [Weave Runtime](/runtimes/weave)
- [Events](/features/events)
