# Kalpataru Development Setup

## Local Development Environment

### Prerequisites

- Node.js 18+
- Docker Desktop or Docker Engine
- PostgreSQL client (optional, for direct DB access)
- Git

### Clone Repository

```bash
git clone https://github.com/vspatabuga/kalpataru-backend-configuration.git
cd kalpataru-backend-configuration
```

### Environment Setup

```bash
# Copy environment file
cp .env.example .env

# Edit .env with your settings
nano .env
```

### Start Development Environment

```bash
# Start all services
docker compose up -d

# View logs
docker compose logs -f

# View API logs specifically
docker compose logs -f api
```

### Database Management

```bash
# Connect to PostgreSQL
docker compose exec db psql -U postgres -d kalpataru

# Run migrations
docker compose exec api npx sequelize-cli db:migrate

# Seed database
docker compose exec api npx sequelize-cli db:seed:all

# Reset database
docker compose exec api npx sequelize-cli db:migrate:undo:all
docker compose exec api npx sequelize-cli db:migrate
docker compose exec api npx sequelize-cli db:seed:undo:all
docker compose exec api npx sequelize-cli db:seed:all
```

### API Development

```bash
# Install dependencies
npm install

# Run in development mode
npm run dev

# Run tests
npm test

# Build for production
npm run build
```

### Testing API

```bash
# Login
curl -X POST http://localhost:3000/api/auth/login \
  -H "Content-Type: application/json" \
  -d '{"email":"ahmad@example.com","password":"demo123"}'

# Get waste catalog
curl http://localhost:3000/api/waste \
  -H "Authorization: Bearer <token>"
```

## Production Deployment

### Build Images

```bash
# Build API image
docker build -t kalpataru-api:latest .

# Build Web image
docker build -t kalpataru-web:latest ./web
```

### Deploy with Docker Compose

```bash
# Use production compose file
docker compose -f docker-compose.yml -f docker-compose.prod.yml up -d
```

### Environment Variables for Production

```bash
# Essential production variables
NODE_ENV=production
DB_HOST=production-db-host
DB_PASSWORD=<strong-password>
JWT_SECRET=<strong-secret>
```

## Troubleshooting

### Container won't start

```bash
# Check logs
docker compose logs api

# Check if ports are available
lsof -i :3000 -i :3001 -i :5432

# Restart services
docker compose restart
```

### Database connection issues

```bash
# Check if database container is running
docker compose ps db

# Check database logs
docker compose logs db

# Verify connection string
docker compose exec api env | grep DB_
```

### Permission issues

```bash
# Fix volume permissions
docker compose down
sudo chown -R $(id -u):$(id -g) ./
docker compose up -d
```
