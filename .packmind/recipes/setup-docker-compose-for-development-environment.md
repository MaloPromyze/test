Configure Docker Compose to set up a complete development environment with database, cache, and application services, enabling consistent local development across team members.

## When to Use

- When setting up a new project that requires multiple services
- When you need to standardize the development environment across the team
- When working with microservices architecture

## Context Validation Checkpoints

* [ ] What services are required (database, Redis, API server, etc.)?
* [ ] What ports should be exposed for local development?
* [ ] Are there any environment-specific configurations needed?
* [ ] What volumes need to be persisted?

## Recipe Steps

### Step 1: Create docker-compose.yml

Create a docker-compose.yml file in the project root with service definitions for all required services including database, cache, and application containers.

```yaml
version: '3.8'
services:
  postgres:
    image: postgres:15
    environment:
      POSTGRES_USER: devuser
      POSTGRES_PASSWORD: devpass
      POSTGRES_DB: myapp
    ports:
      - "5432:5432"
    volumes:
      - postgres_data:/var/lib/postgresql/data

  redis:
    image: redis:7-alpine
    ports:
      - "6379:6379"

  app:
    build: .
    ports:
      - "3000:3000"
    environment:
      DATABASE_URL: postgresql://devuser:devpass@postgres:5432/myapp
      REDIS_URL: redis://redis:6379
    depends_on:
      - postgres
      - redis

volumes:
  postgres_data:
```

### Step 2: Create Dockerfile

Create a Dockerfile for the application service that defines the build process and runtime environment.

```dockerfile
FROM node:18-alpine
WORKDIR /app
COPY package*.json ./
RUN npm ci
COPY . .
RUN npm run build
EXPOSE 3000
CMD ["npm", "start"]
```

### Step 3: Add .dockerignore

Create a .dockerignore file to exclude unnecessary files from the Docker build context, improving build performance.

```
node_modules
npm-debug.log
.git
.env.local
*.md
```

### Step 4: Start Services

Start all services using docker-compose up command and verify all containers are running correctly.

```bash
docker-compose up -d
docker-compose ps
```
