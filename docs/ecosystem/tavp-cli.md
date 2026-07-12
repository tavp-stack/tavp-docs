# tavp-cli

Command line tools untuk TAVP Stack.

## Install

```bash
composer global require tavp/cli
```

## Commands

### Project

| Command | Description |
|---------|-------------|
| `tavp new <name>` | Buat project baru |
| `tavp serve` | Start development server |
| `tavp init` | Init project yang sudah ada |
| `tavp key:generate` | Generate APP_KEY |
| `tavp upgrade` | Upgrade TAVP modules |

### Database

| Command | Description |
|---------|-------------|
| `tavp migrate` | Jalankan migrations |
| `tavp migrate:status` | Cek status migrations |

### Make

| Command | Description |
|---------|-------------|
| `tavp make:model <name>` | Buat model |
| `tavp make:controller <name>` | Buat controller |
| `tavp make:migration <name>` | Buat migration |
| `tavp make:view <name>` | Buat view |
| `tavp make:middleware <name>` | Buat middleware |
| `tavp make:seeder <name>` | Buat seeder |
| `tavp make:event <name>` | Buat event |
| `tavp make:listener <name>` | Buat listener |
| `tavp make:module <name>` | Buat module |
| `tavp make:scaffold <name>` | Buat model + controller + view + migration |

### CMS

| Command | Description |
|---------|-------------|
| `tavp cms:publish` | Publish scheduled content |
| `tavp hub:install` | Install TavpHub admin panel |
| `tavp hub:make:resource` | Buat admin resource |
| `tavp kit:install` | Install TavpKit teams |

### Cache & Schedule

| Command | Description |
|---------|-------------|
| `tavp cache:clear` | Clear application cache |
| `tavp schedule:run` | Run scheduled tasks |

### Environment

| Command | Description |
|---------|-------------|
| `tavp env:list` | List semua environment |
| `tavp env:add <name>` | Tambah environment baru |
| `tavp env:switch <name>` | Switch environment |

### Deploy & Remote

| Command | Description |
|---------|-------------|
| `tavp deploy` | Deploy ke production |
| `tavp push` | Push ke remote |
| `tavp pull` | Pull dari remote |
| `tavp remote:add` | Tambah remote baru |

### Server

| Command | Description |
|---------|-------------|
| `tavp up` | Start server |
| `tavp down` | Maintenance mode |
| `tavp phalcon:install` | Install Phalcon C-extension |
| `tavp weave:enable` | Enable Weave runtime |

## Usage Examples

```bash
# Buat project baru
tavp new my-app

# Start development server
tavp serve

# Jalankan migrations
tavp migrate

# Clear cache
tavp cache:clear

# Publish scheduled content
tavp cms:publish

# Run scheduled tasks
tavp schedule:run
```

## Link

- [GitHub](https://github.com/tavp-stack/tavp-cli)
