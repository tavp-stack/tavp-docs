# tavphub

Admin panel untuk TAVP.

## Fitur

TavpHub adalah "Laravel Nova-nya Phalcon" — **gratis & MIT** (Nova berbayar per project).

- **Auto-generated CRUD** — cukup definisikan 1 `Resource` per model
- **Resource auto-discovery** — scan folder, tak perlu wiring manual
- **Filters** — saring tabel index (select/date/boolean/custom)
- **Metrics** — kartu angka + delta di dashboard & atas tabel
- **Actions** — aksi bulk terhadap baris terpilih
- **Lenses** — tampilan alternatif yang sudah difilter
- **Relationships** — field `belongsTo` jadi dropdown otomatis
- **Policies** — otorisasi per ability (viewAny/view/create/update/delete/...)
- **Search** — pencarian global antar kolom
- **Table & Form builder** — field types, validation, old input
- **UI via tavpblocks** — StatCard, Pagination, Badge, Alert (dengan fallback)

## Install

```bash
composer require tavp/hub
tavp hub:install
```

## Usage

Panduan lengkap: **[TavpHub Admin Panel](/features/tavphub)**.

### Buat Resource

```bash
tavp hub:make:resource Post
```

### Resource Definition

```php
<?php
namespace App\Hub;

use Tavp\Hub\Resource;

class PostResource extends Resource
{
    public function label(): string   { return 'Posts'; }
    public function model(): string   { return \App\Models\Post::class; }

    public function columns(): array
    {
        return [
            ['key' => 'id',    'label' => 'ID',    'sortable' => true],
            ['key' => 'title', 'label' => 'Title', 'sortable' => true],
        ];
    }

    public function fields(): array
    {
        return [
            ['name' => 'title',  'type' => 'text',     'required' => true],
            ['name' => 'status', 'type' => 'select',
             'options' => ['draft', 'published']],
        ];
    }
}
```

### Access Admin Panel

```
http://your-app.com/admin
```

## Link

- [GitHub](https://github.com/tavp-stack/tavphub)
- [Dokumentasi](/features/tavphub)
