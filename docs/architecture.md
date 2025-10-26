# System Architecture

## Overview

DevOps Simulator follows a microservices architecture designed for high availability and scalability. This document covers both production and development configurations.

## Components

### 1. Application Server

- **Technology**: Node.js + Express
- **Production Port**: 8080
- **Development Port**: 3000
- **Scaling**: Horizontal auto-scaling (production), Manual (development)
- **Development Features**: Hot reload, Chrome DevTools debugger on port 9229

### 2. Database Layer

- **Database**: PostgreSQL 14
- **Production**: Master-slave replication with automated daily backups
- **Development**: Single local instance with seed data, manual backups only

### 3. Monitoring System

- **Production**: Prometheus + Grafana with email alerts
- **Development**: Console logging with verbose output, optional Prometheus, build time metrics
- **Metrics**: CPU, Memory, Disk, Network

### 4. Container Orchestration (Development Only)

- **Tool**: Docker Compose
- **Services**: App, Database, Redis cache
- **Volume Mounts**: Code directory for hot reload

### 5. Authentication System (Development Beta)

- **Method**: OAuth2 + JWT
- **Providers**: Google, GitHub (for testing)
- **Sessions**: Redis-based session storage

## Deployment Strategy

### Production

- **Method**: Rolling updates
- **Zero-downtime**: Yes
- **Rollback**: Automated on failure
- **Region**: us-east-1

### Development

- **Method**: Docker Compose hot reload
- **Zero-downtime**: Not applicable
- **Rollback**: Git checkout previous commit
- **Workflow**:
  1. Make code changes
  2. Auto-reload triggers rebuild
  3. Run unit tests
  4. Check console logs
  5. Commit when ready

## Security

- **Production**: SSL/TLS encryption, database connection encryption, regular security audits
- **Development**: SSL/TLS disabled, plain-text credentials, CORS enabled for all origins, debug endpoints exposed

## Experimental Features (Development)

⚠️ **Warning**: These features are experimental:

- Multi-cloud deployment
- AI-powered log analysis
- Automatic rollback on anomaly detection
