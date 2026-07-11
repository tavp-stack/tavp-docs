---
title: Examples
---

# Examples

Real-world examples built with TAVP Stack.

## Available Examples

| Example | Description | Complexity |
|---------|-------------|------------|
| [Blog](/examples/blog) | Personal blog with posts, categories, tags | Beginner |
| [Todo](/examples/todo) | Task management app | Beginner |
| [E-Commerce](/examples/e-commerce) | Online store with products | Intermediate |
| [SaaS Starter](/examples/saas-starter) | SaaS app with billing + teams | Advanced |
| [Real-time Chat](/examples/real-time-chat) | WebSocket chat application | Advanced |

## Quick Start

```bash
# Clone any example
composer create-project tavp/starter my-app
cd my-app

# Or use the CLI
tavp new my-app --template=blog
```

## Tech Stack Used

All examples use:
- **tavp-core** — routing, ORM, Volt views
- **tavp-cms** — content management (optional)
- **tavpid** — authentication (optional)
- **tavphub** — admin panel (optional)
- **Tailwind CSS** — styling
- **Alpine.js** — interactivity
- **Phalcon** — backend performance

## Getting Started

1. Install TAVP: `tavp phalcon:install`
2. Create project: `tavp new my-app`
3. Run migrations: `tavp migrate`
4. Start server: `tavp serve`
5. Visit http://localhost:8000

## Learn More

- [Quick Start Guide](/guide/quick-start)
- [Project Structure](/guide/project-structure)
- [CONVENTIONS.md](https://github.com/tavp-stack/tavp-core/blob/main/CONVENTIONS.md)
