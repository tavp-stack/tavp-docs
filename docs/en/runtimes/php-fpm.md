---
title: PHP-FPM
---

# PHP-FPM Runtime

The default TAVP runtime. Fast, stable, production-ready.

## What is PHP-FPM?

PHP-FPM (FastCGI Process Manager) is the standard way to run PHP on a web server. It manages worker processes and handles incoming requests efficiently.

## How TAVP Uses PHP-FPM

```
HTTP Request → Apache/Nginx → PHP-FPM → TAVP Application
```

TAVP's Phalcon C-extension gives PHP-FPM a massive performance boost:
- **12,000+ requests/second** on a $5 VPS
- **Sub-10ms** page load times
- **Low memory** usage (Phalcon is compiled, not interpreted)

## Setup

### With Lando

```yaml
# .lando.yml
name: my-app
recipe: lamp
config:
  php: '8.3'
  webroot: public
```

```bash
lando start
lando ssh -c "php /app/vendor/bin/tavp phalcon:install"
```

### With Docker

```dockerfile
FROM php:8.3-fpm
RUN apt-get update && apt-get install -y gcc make autoconf
# Install Phalcon...
```

### On VPS

```bash
# Ubuntu/Debian
sudo apt update
sudo apt install php8.3-fpm php8.3-mysql php8.3-mbstring
sudo bash vendor/tavp/tavp-installer/install_phalcon5.sh
sudo service php8.3-fpm restart
```

## Configuration

```ini
; /etc/php/8.3/fpm/php.ini
memory_limit = 256M
max_execution_time = 30
upload_max_filesize = 64M
post_max_size = 64M
```

## Performance Tips

1. **Enable OPcache** — `opcache.enable=1`
2. **Use Phalcon** — C-extension, not interpreted
3. **Cache aggressively** — file cache or Redis
4. **Optimize autoloader** — `composer install --optimize-autoloader`
5. **Enable gzip** — compress responses

## Learn More

- [Installation](/guide/installation)
- [Performance](/reference/performance)
- [TAVP Installer](/ecosystem/tavp-installer)
