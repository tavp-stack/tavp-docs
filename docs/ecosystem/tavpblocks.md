---
title: TavpBlocks
---

# TavpBlocks — UI Components

20 real UI components with Tailwind CSS. Each component renders clean HTML.

## Components

| Component | Description |
|-----------|-------------|
| **Button** | Interactive button (primary/secondary/danger/ghost) |
| **Card** | Content card with title, body, footer |
| **Alert** | Alert messages (info/success/error/warning) |
| **Badge** | Status badges (gray/green/red/yellow/blue) |
| **Modal** | Dialog modal with confirm/cancel |
| **Tabs** | Tab navigation (Alpine.js powered) |
| **Pagination** | Page navigation |
| **StatCard** | Statistics card with trend |
| **Datatable** | Data table with search |
| **Skeleton** | Loading skeleton |
| **Breadcrumb** | Navigation breadcrumb |
| **Accordion** | Collapsible sections |
| **ProgressBar** | Progress indicator |
| **Tooltip** | Hover tooltip |
| **Avatar** | User avatar (image or initials) |
| **EmptyState** | Empty state with action |
| **LoadingSpinner** | Loading spinner |
| **SearchBar** | Search input with icon |
| **NotificationBell** | Notification bell with count |
| **Timeline** | Event timeline |

## Usage in PHP

```php
use Tavp\Blocks\BlockRegistry;

$registry = new BlockRegistry();

// Create a button
$button = $registry->make('Button', [
    'label' => 'Save',
    'variant' => 'primary',
    'href' => '/save'
]);
echo $button->render();

// Create a stat card
$stat = $registry->make('StatCard', [
    'label' => 'Total Users',
    'value' => 1234,
    'trend' => '+12% this month',
    'trendColor' => 'green'
]);
echo $stat->render();

// Create a data table
$table = $registry->make('Datatable');
$table->addColumn('name', 'Name');
$table->addColumn('email', 'Email');
$table->addRow(['name' => 'John', 'email' => 'john@example.com']);
echo $table->render();
```

## Usage in Volt

```php
// Register component helper in ViewFactory
$component = $registry->make('Button', ['label' => 'Click me', 'variant' => 'primary']);
echo $component->render();
```

## Custom Components

Register your own components:

```php
$registry->register('MyButton', \App\Components\MyButton::class);
$button = $registry->make('MyButton', ['label' => 'Custom']);
```
