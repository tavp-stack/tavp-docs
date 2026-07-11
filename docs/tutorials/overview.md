---
title: Tutorials Overview
---

# Tutorials

Step-by-step guides for building with TAVP.

## Available Tutorials

| Tutorial | What You'll Build |
|----------|-------------------|
| [Database](/tutorials/database) | Set up database, run migrations, create models |
| [Authentication](/tutorials/authentication) | Add OTP login with tavpid |
| [API](/tutorials/api) | Build a REST API with headless endpoints |
| [Deployment](/tutorials/deployment) | Deploy to VPS, Docker, or cloud |

## Prerequisites

- PHP 8.3+
- Phalcon 5.16+ (install with `tavp phalcon:install`)
- MySQL/MariaDB or SQLite
- Composer

## Quick Start

```bash
# 1. Create project
composer create-project tavp/starter my-app
cd my-app

# 2. Configure
cp .env.example .env
# Edit .env with your database credentials

# 3. Install Phalcon
tavp phalcon:install

# 4. Run migrations
tavp migrate

# 5. Start development server
tavp serve
```

## Learning Path

1. **Beginner**: [Installation](/guide/installation) → [Quick Start](/guide/quick-start) → [Database Tutorial](/tutorials/database)
2. **Intermediate**: [Authentication](/tutorials/authentication) → [API Tutorial](/tutorials/api) → [Blog Example](/examples/blog)
3. **Advanced**: [Deployment](/tutorials/deployment) → [SaaS Example](/examples/saas-starter) → [Architecture](/architecture/overview)

## Learn More

- [Guide](/guide/what-is-tavp)
- [Examples](/examples/overview)
- [CLI Commands](/reference/cli-commands)
