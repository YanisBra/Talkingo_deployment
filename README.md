# 🛫 Talkingo — Symfony + React (Vite)

Talkingo

## Features

## Getting Started

### Prerequisites

- PHP 
- Node.js 
- Composer
- Mysql
- Docker

### Deploy with Docker (recommanded)

#### Quick setup with Docker Compose

```bash
docker compose up --build -d
docker exec talkingo_backend_container composer install
docker exec talkingo_backend_container php bin/console doctrine:migrations:migrate --no-interaction
docker exec talkingo_backend_container php bin/console lexik:jwt:generate-keypair
```

This will:

- Create a dedicated Docker network (if not exists)
- Start the backend and database services
- Start the frontend 

##### ⚠️ Possible Migration Error

When running the following command:

```bash
docker exec talkingo_backend_container php bin/console doctrine:migrations:migrate --no-interaction
``` 

You might encounter the following error: `SQLSTATE[HY000] [2002] Connection refused`

This usually happens because the database container is not fully ready yet.
Solution: Simply wait a few seconds and re-run the command.

### Deploy locally

#### Backend

##### Install the dependencies

```bash
cd Talkingo_backend
composer install

```

##### Create the database and run the migrations:

Make sure to update the `.env` file if needed

```bash
php bin/console doctrine:database:create
php bin/console doctrine:migrations:migrate
php bin/console lexik:jwt:generate-keypair
```

##### Run the backend locally

```bash
symfony server:start
``` 

The backend will be available at: http://localhost:8082/


#### Frontend

```bash
cd Talkingo_frontend
npm install
npm run dev
```

The frontend will be available at: http://localhost:5173/

## Authentication

- JWT authentication is used.
- The token is stored in localStorage
- Axios interceptors are used to attach the token to every request.