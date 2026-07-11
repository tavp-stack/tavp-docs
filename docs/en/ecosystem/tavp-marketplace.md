---
title: Tavp Marketplace
---

# Tavp Marketplace

Module and theme marketplace for TAVP.

## Status

⚠️ **Early stage** — classes exist, marketplace API planned.

## What Exists

```php
use Tavp\Marketplace\ModuleMarketplace;

$marketplace = new ModuleMarketplace(['api_url' => 'https://marketplace.tavp.dev/api']);

// Search for modules
$results = $marketplace->search('blog');

// Get module details
$module = $marketplace->get('tavp-cms');
```

## Planned Features

| Feature | Description | Status |
|---------|-------------|--------|
| Module search | Search published modules | Planned |
| Module install | Install via composer | Planned |
| Module publish | Publish your modules | Planned |
| Theme marketplace | Buy/sell themes | Planned |
| Revenue sharing | Earn from modules | Planned |

## For Now

Use **Composer** to install TAVP modules:

```bash
composer require tavp/tavp-cms
composer require tavp/tavpid
composer require tavp/tavphub
```

## Publish Your Module

When the marketplace is ready:

```bash
tavp marketplace:publish my-module
```

## Link

- [GitHub](https://github.com/tavp-stack/tavp-marketplace)
