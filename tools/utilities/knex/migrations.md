# Migrations

## Create

```bash
knex migrate:make migration_name -x ts
```

This will create the file RANDOM-NUMBER\_migration\_name.ts

```typescript
export async function up(knex: Knex): Promise<void> {
}


export async function down(knex: Knex): Promise<void> {
}
```

## Latest

```bash
npx knex migrate:latest
```

## Rollback

```bash
npx knex migrate:rollback
```

or

```bash
npx knex migrate:rollback --all
```

## Up/Down

```bash
npx knex migrate:up
```

or

```bash
npx knex migrate:down
```

## List

```bash
npx knex migrate:list
```

## Example

```typescript
import {Knex} from "knex";
import {tableNames} from "../../src/constants/table-names";


export async function up(knex: Knex): Promise<void> {
    await knex.schema.createTable(tableNames.user, table => {
        table.increments().notNullable();
        table.string('email', 255).notNullable().unique();
        table.string('first_name', 255).notNullable();
        table.string('last_name', 255).notNullable();
        table.string('password', 255).notNullable();
        table.dateTime('last_login');
    });
}


export async function down(knex: Knex): Promise<void> {
    await knex.schema.dropTable(tableNames.user);
}
```
