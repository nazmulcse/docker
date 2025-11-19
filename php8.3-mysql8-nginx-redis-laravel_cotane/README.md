# Laravel Octane with Docker

## Installation Instructions

### Step 1: Copy Docker Files
Copy the following files into the **root folder** of your Laravel project:

- `docker-compose.yml`
- `Dockerfile`
- `nginx.conf`

---

### Step 2: Start Docker Containers
Run the containers:

```bash
sudo docker compose up -d
```

### Step 3: Install and start Laravel Octane

```bash
sudo docker compose exec app composer require laravel/octane
sudo docker compose exec app php artisan octane:install
sudo docker compose exec app php artisan octane:start --host=0.0.0.0 --port=8000
```

### Run Octane start command in brackground

```bash
sudo docker compose exec -d app php artisan octane:start --host=0.0.0.0 --port=8000		## Only added -d flag after exec
