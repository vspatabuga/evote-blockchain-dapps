# Blockchain Ledger Simulation

> Immutable Voting System - Simulation Guide

## Overview

Blockchain Ledger is a decentralized voting application demonstrating Ethereum smart contracts for secure, transparent, and immutable elections. This simulation allows you to experience a complete blockchain voting system locally.

## Prerequisites

- Docker 20.10+
- Docker Compose v2+
- Node.js 18+
- 4GB+ RAM recommended

## Quick Start

### Option 1: Using vsp-porto (Recommended)

```bash
# Install vsp-porto
curl -fsSL https://porto.vspatabuga.io/ | sh

# Install Blockchain Ledger simulation
vsp-porto install ledger

# Start the simulation
vsp-porto start ledger -o

# View logs
vsp-porto logs ledger -f
```

### Option 2: Direct Docker

```bash
git clone https://github.com/vspatabuga/evote-blockchain-dapps.git
cd evote-blockchain-dapps
./simulate.sh
```

## Access URLs

| Service | URL | Description |
|---------|-----|-------------|
| Web UI | http://localhost:3000 | Voting application |
| API | http://localhost:3001 | Backend API |
| Blockchain (Ganache) | http://localhost:8545 | Local Ethereum node |

## Features

- **Immutable Ledger** - Permanent vote recording on blockchain
- **Smart Contract Governance** - Hard-coded voting rules
- **DApp Interface** - Web3-enabled voting interface
- **Election Management** - Create and manage elections
- **Real-time Results** - Live vote tallying

## Components

### Ganache
Local Ethereum blockchain for development and testing.

### API Server
Express.js backend handling business logic and blockchain interactions.

### Web Client
React application with Web3 integration for voting.

## Demo Workflow

1. **Create Election** - Admin creates a new election
2. **Authorize Voters** - Add voter addresses
3. **Cast Votes** - Voters submit votes
4. **View Results** - Real-time vote counting

## Stopping the Simulation

```bash
# Using vsp-porto
vsp-porto stop ledger

# Or using docker-compose
docker compose -p vsp-ledger down
```

## Troubleshooting

### Metamask connection issues

```bash
# Add Ganache to Metamask
# Network Name: Local Ganache
# RPC URL: http://localhost:8545
# Chain ID: 1337
# Currency Symbol: ETH
```

### Contract deployment issues

```bash
# Redeploy contracts
cd contracts
npm install
npx truffle migrate --reset
```

## Documentation

- [Architecture](./ARCHITECTURE.md)
- [Development Setup](./SETUP.md)
