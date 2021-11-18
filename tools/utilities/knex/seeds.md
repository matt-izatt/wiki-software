# Seeds

## Create

```bash
npx knex seed:make seed_name
```

## Run

```bash
npx knex seed:run
```

## Example

```typescript
import {Knex} from "knex";
import {tableNames} from "../../../src/constants/table-names";


export async function seed(knex: Knex): Promise<void> {
    await knex(tableNames.user).del();

    await knex(tableNames.user).insert([
        {
            email: "john.smith@gmail.com",
            first_name: 'John',
            last_name: 'Smith',
            password: 'password'
        },
        {
            email: "alan.jones@gmail.com",
            first_name: 'Alan',
            last_name: 'Jones',
            password: 'password'
        }
    ]);
}
```
