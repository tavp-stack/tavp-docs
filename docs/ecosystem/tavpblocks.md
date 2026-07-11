---
title: TavpBlocks
---

# TavpBlocks — UI Components

UI component library for TAVP. Currently in early development.

## Status

⚠️ **Early stage** — BlockRegistry exists, full component library planned.

## What Exists

```php
// BlockRegistry — register and render blocks
use Tavp\Blocks\BlockRegistry;

$registry = new BlockRegistry();
$registry->register('button', fn ($props) => '<button>' . $props['label'] . '</button>');
```

## Planned Components

| Component | Description | Status |
|-----------|-------------|--------|
| Button | Interactive button | Planned |
| Card | Content card | Planned |
| Modal | Dialog modal | Planned |
| Form | Form builder | Planned |
| Table | Data table | Planned |
| Tabs | Tab navigation | Planned |
| Alert | Alert messages | Planned |
| Badge | Status badges | Planned |
| Dropdown | Dropdown menu | Planned |
| Sidebar | Side navigation | Planned |

## Usage (when available)

```php
// In Volt template
<x-button label="Click me" variant="primary" />
<x-card title="Hello">
    <p>Content here</p>
</x-card>
```

## Alternative

For now, use **TavpHub** (`tavp/tavphub`) for admin UI components:

- `FormBuilder` — form rendering with validation
- `TableBuilder` — data table rendering
- `Resource` — CRUD resource definition

## Link

- [TavpHub](/ecosystem/tavphub)
- [GitHub](https://github.com/tavp-stack/tavpblocks)
