# 🔥 Social Network API

[![Python](https://img.shields.io/badge/Python-3.10-blue.svg)](https://www.python.org/)
[![Django](https://img.shields.io/badge/Django-5.2-green.svg)](https://www.djangoproject.com/)
[![DRF](https://img.shields.io/badge/DRF-3.15-red.svg)](https://www.django-rest-framework.org/)
[![Docker](https://img.shields.io/badge/Docker-28.0+-blue.svg)](https://www.docker.com/)
[![MySQL](https://img.shields.io/badge/MySQL-8.0-orange.svg)](https://www.mysql.com/)
[![JWT](https://img.shields.io/badge/JWT-Auth-purple.svg)](https://jwt.io/)
[![License](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)

> A production-grade social network backend API built with Django REST Framework, containerized with Docker, and secured with JWT authentication.

## 📋 Table of Contents

- [✨ Features](#-features)
- [🛠️ Tech Stack](#️-tech-stack)
- [🏗️ Architecture](#️-architecture)
- [📂 Project Structure](#-project-structure)
- [🚦 Quick Start](#-quick-start)
- [🐳 Docker Services](#-docker-services)
- [🔐 Environment Variables](#-environment-variables)
- [🤝 Contributing](#-contributing)
- [📄 License](#-license)
- [👤 Author](#-author)

---

## ✨ Features

| Category | Features |
|----------|----------|
| 🔐 Authentication | JWT-based auth, registration, login, profile management |
| 👥 Social | Friend requests, accept/decline, friend lists |
| 📝 Posts | Create, edit, delete posts, like/unlike, comment |
| 🐳 DevOps | Docker orchestration, Nginx reverse proxy, uWSGI |
| 🛡️ Security | Environment variables, CORS ready, SQL injection protected |

---

## 🛠️ Tech Stack

| Layer | Technology |
|-------|------------|
| Backend | Django 5.2, Django REST Framework |
| Database | MySQL 8.0 |
| Auth | JWT (Simple JWT) |
| Server | Nginx + uWSGI |
| Container | Docker + Docker Compose |
| Language | Python 3.10 |

---
## 🏗️ Architecture

```
Client
       │
       ▼
┌──────────────┐
│    Nginx     │  :80 (reverse proxy + static/media)
│   (Proxy)    │
└──────┬───────┘
       │
       ▼
┌──────────────┐
│    uWSGI     │  :8000 (application server)
│   (WSGI)     │
└──────┬───────┘
       │
       ▼
┌──────────────┐
│    Django    │  (business logic)
│     API      │
└──────┬───────┘
       │
       ▼
┌──────────────┐
│    MySQL     │  :3306 (database)
└──────────────┘
```
---
## 📂 Project Structure

```bash
social_network/
├── accounts/                 # User management app
├── friendship/               # Friend system app
├── posts/                    # Posts & interactions app
├── social_network/           # Project core settings
│   ├── settings.py
│   ├── urls.py
│   ├── local_settings.py.example
│   └── wsgi.py
├── deploy/                   # Docker & server configs
│   ├── Dockerfile-base
│   ├── Dockerfile-requirements
│   ├── nginx.conf
│   └── uwsgi.ini
├── static/                   # Collected static files
├── media/                    # User uploaded files
├── manage.py
├── docker-compose.yml
├── pyproject.toml
└── README.md
```
---

🚦 Quick Start

🐳 Docker (Production)

```bash
# 1. Clone the repository
git clone https://github.com/HosseinGhasemii/social_network.git
cd social_network

# 2. Build images (no cache for clean build)
docker-compose build --no-cache

# 3. Run containers in detached mode
docker-compose up -d

# 4. Run database migrations
docker exec -it social_network-server-1 python manage.py migrate

# 5. Create admin user
docker exec -it social_network-server-1 python manage.py createsuperuser

# 6. Collect static files
docker exec -it social_network-server-1 python manage.py collectstatic --noinput

# 7. Access the application
# Open http://localhost in your browser
```
---

💻 Local Development

```bash
# 1. Create virtual environment
python -m venv venv
source venv/bin/activate      # Linux/macOS
venv\Scripts\activate         # Windows

# 2. Install dependencies
pip install -e .

# 3. Copy settings example
cp social_network/local_settings.py.example social_network/local_settings.py

# 4. Run migrations
python manage.py migrate

# 5. Create superuser
python manage.py createsuperuser

# 6. Run development server
python manage.py runserver
```
---
🐳 Docker Services

Service Port Internal Port Description
nginx 80 80 Reverse proxy, static/media serving
server - 8000 Django + uWSGI application
db 3306 3306 MySQL database

Useful Docker Commands

```bash
# View logs
docker-compose logs -f nginx
docker-compose logs -f server

# Stop all services
docker-compose down

# Restart a specific service
docker-compose restart server

# Access database directly
docker exec -it social_network-db-1 mysql -u root -p
```
---
🔐 Environment Variables

Create local_settings.py from the example file:

```python
# Database configuration
DATABASES = {
    'default': {
        'ENGINE': 'django.db.backends.mysql',
        'NAME': 'social_network',
        'USER': 'social_network_user',
        'PASSWORD': 'your_secure_password',
        'HOST': 'db',
        'PORT': '3306',
    }
}

# Security
SECRET_KEY = 'your-secret-key-here'
DEBUG = False
ALLOWED_HOSTS = ['localhost', 'your-domain.com']
```

⚠️ Never commit local_settings.py to version control!

---

📡 API Endpoints

Method Endpoint Description
POST /api/auth/register/ User registration
POST /api/auth/login/ JWT login
GET /api/auth/profile/ User profile
GET /api/friends/ Friend list
POST /api/friends/request/ Send friend request
GET /api/posts/ List posts
POST /api/posts/ Create post
POST /api/posts/<id>/like/ Like/unlike post

Full Postman collection available upon request.

---

🤝 Contributing

Contributions are welcome! Please follow these steps:

1. Fork the repository
2. Create a feature branch (git checkout -b feature/amazing-feature)
3. Commit your changes (git commit -m 'Add some amazing feature')
4. Push to the branch (git push origin feature/amazing-feature)
5. Open a Pull Request

Development Guidelines

· Follow PEP 8 style guide
· Write docstrings for new functions
· Add tests for new features
· Update README if needed

---

📄 License

Distributed under the MIT License. See LICENSE file for more information.

```
MIT License

Copyright (c) 2026 Hossein Ghasemi

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files...
```

---

👤 Author

Hossein Ghasemi

· GitHub: @HosseinGhasemii
· Email: (qasmyh094@gmail.com)

---

⭐ Show Your Support

If this project helped you or you found it useful, please give it a star!

https://img.shields.io/github/stars/HosseinGhasemii/Social_Network.svg?style=social

---

Built with 🐍 Django and ☕ late nights.
