---
layout: home
title: TAVP Stack — PHP, but fast.
description: "TAVP is a curated PHP tech stack combining Tailwind CSS, Alpine.js, Volt, and Phalcon for high-performance web applications."

hero:
  name: TAVP Stack
  text: PHP, but fast.
  tagline: "Tailwind CSS + Alpine.js + Volt + Phalcon — a curated tech stack, not a framework."
  image:
    src: /logo.png
    alt: TAVP Stack
  actions:
    - theme: brand
      text: Mulai Sekarang
      link: /guide/what-is-tavp
    - theme: alt
      text: Lihat di GitHub
      link: https://github.com/tavp-stack

features:
  - title: 12,000+ Requests/sec
    details: "Phalcon C-extension memberikan performa yang luar biasa tanpa mengorbankan developer experience. Compiled, bukan interpreted."
  - title: 124+ UI Components
    details: "TAVPblocks menyediakan 124+ komponen siap pakai dengan Tailwind CSS + DaisyUI + Chart.js."
  - title: OTP Authentication
    details: "Login tanpa password via Email, SMS, WhatsApp. JWT API auth built-in. Role & Permission (RBAC) included."
  - title: 4 Runtime Options
    details: "PHP-FPM, TAVP Coil (Swoole), TAVP Relay (RoadRunner), TAVP Weave (PHP Fibers). Semua share code yang sama."
  - title: AI Integration
    details: "OpenAI, Anthropic, Ollama. Generate kode, tulis konten, bangun chatbot."
  - title: Module Marketplace
    details: "Publish dan gunakan module dari komunitas. Composer-based packages."
---

<div class="benchmark-grid">
  <div class="benchmark-card">
    <div class="value">12,000+</div>
    <div class="label">req/s</div>
    <div class="desc">Phalcon C-Extension — raw PHP requests per second</div>
  </div>
  <div class="benchmark-card">
    <div class="value">&lt;10ms</div>
    <div class="label">Response Time</div>
    <div class="desc">Average response time with Phalcon</div>
  </div>
  <div class="benchmark-card">
    <div class="value">12+</div>
    <div class="label">Core Modules</div>
    <div class="desc">Modular ecosystem — pick what you need</div>
  </div>
  <div class="benchmark-card">
    <div class="value">124+</div>
    <div class="label">UI Components</div>
    <div class="desc">Tailwind + DaisyUI + Chart.js — all included</div>
  </div>
</div>

## Tech Stack

| Technology | Role |
|------------|------|
| **[Tailwind CSS](https://tailwindcss.com/)** | Utility-first CSS framework for rapid UI development |
| **[Alpine.js](https://alpinejs.dev/)** | Lightweight JavaScript framework for interactivity |
| **[Volt](https://phalcon.io/en-us)** | Ultra-fast templating engine (Phalcon C-extension) |
| **[Phalcon](https://phalcon.io/en-us)** | High-performance PHP framework (C-extension) |