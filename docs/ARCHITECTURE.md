# Kalpataru Architecture

## System Overview

```
┌─────────────────────────────────────────────────────────────────────────┐
│                           CLIENT LAYER                                  │
│                    (React/Web - Port 3001)                              │
└─────────────────────────────────────────────────────────────────────────┘
                                    │
                                    ▼
┌─────────────────────────────────────────────────────────────────────────┐
│                            API LAYER                                    │
│                   (Express.js - Port 3000)                              │
│  ┌──────────────┐  ┌──────────────┐  ┌──────────────┐                  │
│  │   Auth API   │  │  Waste API   │  │  Wallet API  │                  │
│  └──────────────┘  └──────────────┘  └──────────────┘                  │
└─────────────────────────────────────────────────────────────────────────┘
                                    │
                                    ▼
┌─────────────────────────────────────────────────────────────────────────┐
│                          DATA LAYER                                     │
│                    (PostgreSQL - Port 5432)                            │
│  ┌──────────────┐  ┌──────────────┐  ┌──────────────┐                  │
│  │    users     │  │  waste_items │  │ transactions │                  │
│  └──────────────┘  └──────────────┘  └──────────────┘                  │
└─────────────────────────────────────────────────────────────────────────┘
```

## Components

### Web Client (Port 3001)
- Nginx serving static React application
- API communication with backend
- Responsive UI for mobile and desktop

### API Server (Port 3000)
- Express.js REST API
- JWT authentication
- Sequelize ORM for database operations
- Request validation and error handling

### Database (Port 5432)
- PostgreSQL 15 Alpine
- Persistent volume for data
- Initialized with seed data

## API Endpoints

### Authentication
| Method | Endpoint | Description |
|--------|----------|-------------|
| POST | /api/auth/login | User login |
| POST | /api/auth/register | User registration |
| GET | /api/auth/profile | Get current user |

### Waste Catalog
| Method | Endpoint | Description |
|--------|----------|-------------|
| GET | /api/waste | List all waste types |
| GET | /api/waste/:id | Get waste type details |

### Transactions
| Method | Endpoint | Description |
|--------|----------|-------------|
| POST | /api/transactions | Create transaction |
| GET | /api/transactions | List user transactions |
| GET | /api/transactions/:id | Get transaction details |

## Data Models

### User
```
id: UUID (primary key)
email: string (unique)
password: string (hashed)
name: string
role: enum (member, operator, admin)
balance: decimal
createdAt: timestamp
updatedAt: timestamp
```

### WasteItem
```
id: UUID (primary key)
type: string (plastic, paper, metal, glass, etc.)
name: string
description: string
pricePerKg: decimal
unit: string (kg)
imageUrl: string
createdAt: timestamp
```

### Transaction
```
id: UUID (primary key)
userId: UUID (foreign key)
operatorId: UUID (foreign key)
totalAmount: decimal
status: enum (pending, completed, cancelled)
createdAt: timestamp
```

## Security

- Password hashing with bcrypt
- JWT token-based authentication
- Role-based access control (RBAC)
- Input validation and sanitization
- CORS configuration

## Environment Variables

```bash
# Database
DB_HOST=db
DB_PORT=5432
DB_NAME=kalpataru
DB_USER=postgres
DB_PASSWORD=kalpataru123

# Application
PORT=3000
JWT_SECRET=your-secret-key
JWT_EXPIRES_IN=24h
```
