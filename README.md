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

3. Start PostgreSQL locally (no Docker needed):

```bash
# run your preferred PostgreSQL instance and set DATABASE_URL in .env
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
npm run db:deploy
npm run db:seed
npm run db:studio
```

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


