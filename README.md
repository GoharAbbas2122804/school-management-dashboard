# GoharAbbas Dev School Management Dashboard

## Getting Started

1. Install dependencies:

```bash
npm install
```

2. Copy the environment file and update the values:

```bash
cp .env.example .env
```

3. Configure your database connection:

```bash
# for Supabase, set DATABASE_URL and DIRECT_DATABASE_URL in .env
```

4. Generate Prisma client, run migrations, and seed the database:

```bash
npm run db:generate
npm run db:migrate
npm run db:seed
```

5. Start the app:

```bash
npm run dev
```

Open [http://localhost:3000](http://localhost:3000) with your browser to see the result.

## Prisma Commands

```bash
npm run db:generate
npm run db:migrate
npm run db:migrate:dev
npm run db:deploy
npm run db:push
npm run db:seed
npm run db:setup
npm run db:studio
```

## Supabase Setup

This project can use Supabase as its hosted Postgres database.

1. Create a Supabase project.
2. In the Supabase SQL Editor, create a dedicated Prisma user:

```sql
create user "prisma" with password 'your_prisma_password' bypassrls createdb;
grant "prisma" to "postgres";
grant usage on schema public to prisma;
grant create on schema public to prisma;
grant all on all tables in schema public to prisma;
grant all on all routines in schema public to prisma;
grant all on all sequences in schema public to prisma;
alter default privileges for role postgres in schema public grant all on tables to prisma;
alter default privileges for role postgres in schema public grant all on routines to prisma;
alter default privileges for role postgres in schema public grant all on sequences to prisma;
```

3. Open the Supabase database **Connect** page.
4. Set `.env` like this:

```bash
DATABASE_URL="postgresql://prisma.<project-ref>:<prisma-password>@<region>.pooler.supabase.com:5432/postgres?sslmode=require"
```

Notes:
- `DATABASE_URL` should use the Supavisor session pooler on port `5432`.
- For local IPv4-only development, prefer the pooler string instead of the direct `db.<project-ref>.supabase.co` host.
- `npm run db:migrate` in this project is configured for remote-safe `prisma migrate deploy`.

## Clerk Setup

This project already uses Clerk in the App Router with:

- `clerkMiddleware()` in [src/middleware.ts](./src/middleware.ts)
- `ClerkProvider` in [src/app/layout.tsx](./src/app/layout.tsx)
- a custom sign-in page in [src/app/[[...sign-in]]/page.tsx](./src/app/[[...sign-in]]/page.tsx)

### Local development

Clerk supports keyless mode for local setup. If you want to use it, leave these env vars empty in `.env`:

```bash
NEXT_PUBLIC_CLERK_PUBLISHABLE_KEY=""
CLERK_SECRET_KEY=""
```

Then run:

```bash
npm run dev
```

Clerk will show a "Configure your application" prompt in development. You can claim it later from the Clerk dashboard.

### Using your own Clerk project

1. Create a Clerk application in the Clerk dashboard.
2. Open the app's **API Keys** page.
3. Copy:
   - `NEXT_PUBLIC_CLERK_PUBLISHABLE_KEY`
   - `CLERK_SECRET_KEY`
4. Paste them into `.env` locally and into your hosting provider's environment variables for production.

## Cloudinary Setup

This project uses `next-cloudinary` and expects:

```bash
NEXT_PUBLIC_CLOUDINARY_CLOUD_NAME=""
```

It also uses an unsigned upload preset named `school` in the student form. In Cloudinary:

1. Create or open your Cloudinary product environment.
2. Copy the **Cloud name** from the dashboard into `NEXT_PUBLIC_CLOUDINARY_CLOUD_NAME`.
3. Create an **unsigned** upload preset named `school`.
