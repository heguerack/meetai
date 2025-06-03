# Franks notes

for all install check your version! like @n.n.n

## Install shadcd

npx shadcn@latest init

### install all shadcn compinets at once

npx shadcn@2.5.0 add --all

## Github - branching

click source control icon
click on plus icon in changes tab
once changes are staged, enter a commit message, and hit comit

### create new repo iin github

push an existing repository from the command line

```js
git remote add origin https://github.com/heguerack/meetai.git
git branch -M main
git push -u origin main
```

## Add neon postgres Database

create project
grag connection string and add to .env
make sure the .env is a bit gray, meaning is added to .gitignore

## Add drizzle ORM

```ts
https://orm.drizzle.team/docs/get-started/neon-new
```

```ts
npm i drizzle-orm pg
```

but in this case we will install the following as we are using neon,

```ts
https://orm.drizzle.team/docs/get-started/neon-new
```

```ts
npm i drizzle-orm @neondatabase/serverless dotenv
npm i drizzle-orm@0.43.1 @neondatabase/serverless@1.0.0 dotenv@16.5.0  --legacy-peer-deps

```

```ts
npm i -D drizzle-kit
npm i -D drizzle-kit@0.31.1 --legacy-peer-deps tsx@4.19.4 --legacy-peer-deps

```

### Connect drizzle to the databse

Create a index.ts file in the src/db directory and initialize the connection:

```ts
import { drizzle } from 'drizzle-orm/neon-http'

const db = drizzle(process.env.DATABASE_URL)
```

### create a table

```ts
import { integer, pgTable, varchar } from 'drizzle-orm/pg-core'

export const usersTable = pgTable('users', {
  id: integer().primaryKey().generatedAlwaysAsIdentity(),
  name: varchar({ length: 255 }).notNull(),
  age: integer().notNull(),
  email: varchar({ length: 255 }).notNull().unique(),
})
```

### Set up a drizzle config file

Create a drizzle.config.ts file in the root of your project and add the following content:

```ts
import 'dotenv/config'
import { defineConfig } from 'drizzle-kit'

export default defineConfig({
  out: './drizzle',
  schema: './src/db/schema.ts',
  dialect: 'postgresql',
  dbCredentials: {
    url: process.env.DATABASE_URL!,
  },
})
```

### Applying changes to the database

You can directly apply changes to your database using the drizzle-kit push command. This is a convenient method for quickly testing new schema designs or modifications in a local development environment, allowing for rapid iterations without the need to manage migration files:

```ts
npx drizzle-kit push
```

### set up drizzle studio

```ts
npx drizzle-kit studio
```

### create shorcuts in packge json

"db-push": "drizzle-kit push",
"db:studio": "drizzle-kit studio"

## second push!!
