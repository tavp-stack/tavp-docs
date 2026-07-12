---
title: Tavp Installer
---

# TAVP Installer

Install Phalcon C-extension on any system.

## Quick Start

```bash
# Via TAVP CLI (recommended)
tavp phalcon:install

# Or directly
sudo bash vendor/tavp/tavp-installer/install_phalcon5.sh
```

## What It Does

1. Detects PHP version
2. Installs build dependencies
3. Downloads Phalcon source
4. Compiles extension (~5-7 minutes)
5. Enables extension in php.ini
6. Verifies installation

## Supported Systems

- Ubuntu 20.04 / 22.04 / 24.04
- Debian 11 / 12
- Lando containers
- Docker (Debian-based)

## Requirements

- PHP 8.1+
- Root access (sudo)
- Build tools (gcc, make, autoconf)

## Pin Version

```bash
# Pin PHP version
sudo bash install_phalcon5.sh 8.3

# Pin PHP + Phalcon version
sudo bash install_phalcon5.sh 8.3 5.16.0
```

## Verify

```bash
php -m | grep phalcon
php -r "echo phpversion('phalcon');"
```

## Troubleshooting

### "phalcon.so not found"

```bash
# Check extension dir
php -i | grep extension_dir

# Check if ini exists
ls /etc/php/*/conf.d/*phalcon.ini
```

### "Permission denied"

```bash
sudo bash install_phalcon5.sh
```

## Lando (Local Development)

When using Lando for local development, Phalcon survives container rebuilds if configured correctly.

### Auto-load Phalcon

Create `.lando.php.ini` in your project root:

```ini
; Auto-load Phalcon extension (survives rebuilds)
extension=phalcon.so
```

Add to `.lando.yml`:

```yaml
config:
  php: '8.3'
  conf:
    php: .lando.php.ini
```

### Install Phalcon

```bash
# Rebuild first (clean state)
lando rebuild -y

# Install Phalcon (requires root inside container)
lando ssh -u root -c "bash /app/vendor/tavp/cli/scripts/install-phalcon.sh"

# Verify
lando ssh -c "php -m | grep -i phalcon"
```

### After Rebuild

```bash
lando rebuild -y
lando ssh -u root -c "bash /app/vendor/tavp/cli/scripts/install-phalcon.sh"
```

The `.lando.php.ini` file ensures Phalcon loads on every rebuild. Without it, you must manually reinstall after every `lando rebuild`.

## Link

- [Installation Guide](/guide/installation)
- [GitHub](https://github.com/tavp-stack/tavp-installer)
