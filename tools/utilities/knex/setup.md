# Setup

## Installation

### Knex

```bash
npm install knex
```

### TS-Node

```bash
npm install --save-dev ts-node
```

### Postgres Driver

```bash
npm install pg
```

### Initialise

```bash
npx knex init -x ts
```

## Configuration

### Basic

Basic knexfile setup:

```typescript
const config = {

    development: {
        client: 'pg',
        connection: {
            host: process.env.POSTGRES_HOST,
            port: process.env.POSTGRES_PORT,
            database: process.env.POSTGRES_DB,
            user: process.env.POSTGRES_USER,
            password: process.env.POSTGRES_PASSWORD
        }
    }

};

export default config;
```

### Migrations

```typescript
const config = {

    development: {
        client: 'pg',
        connection: {
            host: process.env.POSTGRES_HOST,
            port: process.env.POSTGRES_PORT,
            database: process.env.POSTGRES_DB,
            user: process.env.POSTGRES_USER,
            password: process.env.POSTGRES_PASSWORD
        },
        migrations: {
            directory: './db/migrations'
        }
    }

};

export default config;
```

### Seeds

```typescript
const config = {

    development: {
        client: 'pg',
        connection: {
            host: process.env.POSTGRES_HOST,
            port: process.env.POSTGRES_PORT,
            database: process.env.POSTGRES_DB,
            user: process.env.POSTGRES_USER,
            password: process.env.POSTGRES_PASSWORD
        },
        migrations: {
            directory: './db/migrations'
        },
        seeds: {
            directory: './db/seeds/dev'
        }
    }

};

export default config;
```

