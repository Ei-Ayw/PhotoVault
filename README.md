<div align="center">

# PhotoVault

**Full-Stack Photo Gallery with Watermark, Admin Panel & AWS Deployment**

基于 Laravel 11 的全栈相册管理系统

[![Laravel](https://img.shields.io/badge/Laravel-11-FF2D20?style=flat-square&logo=laravel&logoColor=white)](https://laravel.com)
[![PHP](https://img.shields.io/badge/PHP-8.2+-777BB4?style=flat-square&logo=php&logoColor=white)](https://php.net)
[![Tailwind CSS](https://img.shields.io/badge/Tailwind-3-06B6D4?style=flat-square&logo=tailwindcss&logoColor=white)](https://tailwindcss.com)
[![License: MIT](https://img.shields.io/badge/License-MIT-green?style=flat-square)](LICENSE)

</div>

---

## Overview

PhotoVault is a full-stack photo management application built with **Laravel 11 + Tailwind CSS**. It provides a complete photo gallery experience with upload, watermark generation, admin management, user authentication, and one-click AWS deployment support.

---

## Architecture

```mermaid
graph TB
    subgraph Frontend ["Frontend (Blade + Tailwind)"]
        GALLERY[Photo Gallery]
        UPLOAD[Upload & Edit]
        AUTH[Auth Pages]
        ADMIN[Admin Dashboard]
    end

    subgraph Backend ["Backend (Laravel 11)"]
        CTRL[Controllers]
        POLICY[Policies & Middleware]
        MODEL[Eloquent Models]
        WM[Watermark Service]
        STORE[File Storage]
    end

    subgraph Infra ["Infrastructure"]
        DB[(MySQL / SQLite)]
        S3[AWS S3]
        QUEUE[Job Queue]
    end

    GALLERY --> CTRL
    UPLOAD --> CTRL
    AUTH --> CTRL
    ADMIN --> POLICY
    POLICY --> CTRL
    CTRL --> MODEL
    CTRL --> WM
    CTRL --> STORE
    MODEL --> DB
    STORE --> S3

    style Frontend fill:#1e293b,stroke:#334155,color:#fff
    style Backend fill:#FF2D20,stroke:#333,color:#fff
    style Infra fill:#164e63,stroke:#334155,color:#fff
```

---

## Features

- **Photo Management** — Upload, view, edit, and delete photos with metadata
- **Watermark Engine** — Automatic watermark generation on uploaded images
- **Admin Panel** — Full admin dashboard for user and photo management
- **User Authentication** — Registration, login, email verification (Laravel Breeze)
- **Role-Based Access** — Admin middleware with policy-based authorization
- **AWS Deployment** — Pre-configured deployment scripts for AWS EC2 + S3
- **Responsive UI** — Tailwind CSS dark/light theme with mobile support

---

## Screenshots

<!-- TODO: Add screenshots of the gallery and admin panel -->
> Screenshots coming soon.

---

## Quick Start

### Prerequisites

- PHP 8.2+
- Composer
- Node.js 18+
- MySQL (or SQLite for development)

### Install & Run

```bash
git clone https://github.com/Ei-Ayw/PhotoVault.git
cd PhotoVault

# Install dependencies
composer install
npm install

# Configure environment
cp .env.example .env
php artisan key:generate

# Database setup
php artisan migrate --seed

# Build frontend assets
npm run build

# Start development server
php artisan serve
# Open http://localhost:8000
```

---

## Tech Stack

| Layer | Technology |
|-------|-----------|
| **Backend** | Laravel 11, PHP 8.2 |
| **Frontend** | Blade Templates, Tailwind CSS, Vite |
| **Database** | MySQL / SQLite |
| **Auth** | Laravel Breeze |
| **Storage** | Local / AWS S3 |
| **Testing** | PHPUnit |

---

## License

This project is licensed under the MIT License.

