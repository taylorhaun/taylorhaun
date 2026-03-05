# Database & Auth Research

*Research compiled March 2026 for the Music Collaborator custom build.*

---

## Database Options

### Neon (PostgreSQL) — RECOMMENDED

- **What**: Serverless PostgreSQL that scales to zero
- **Free tier**: 0.5 GB storage, 20 projects
- **Pros**:
  - Full PostgreSQL (JSONB, full-text search, extensions, stored procedures)
  - Database branching (instant copies for testing/CI)
  - Scales to zero when idle, wakes in milliseconds
  - Great DX, works seamlessly with Drizzle and Prisma
  - Region-based, fast for single-region apps
- **Cons**:
  - ~500ms cold start on first query after idle
  - 0.5 GB free tier is tight for heavy usage
  - No global edge replication (region-based only)
- **Paid**: Starts at $19/month
- **Best for**: Full Postgres apps, CI/CD workflows, Next.js projects

### Turso (libSQL / SQLite)

- **What**: Edge-distributed SQLite (libSQL fork)
- **Free tier**: 5 GB storage, 100 databases, 500M row reads/month
- **Pros**:
  - Most generous free tier by far
  - Global edge replicas = sub-10ms reads when co-located
  - Tiny client, great for serverless/edge
  - Works well with Drizzle ORM
- **Cons**:
  - SQLite limitations (no stored procedures, fewer data types)
  - Single-writer architecture (concurrent writes added 2025 but still limited)
  - Less ecosystem tooling than Postgres
  - Deprecated "scale to zero" for new users (Jan 2026)
- **Best for**: Read-heavy apps, edge computing, budget-conscious projects

### Vercel Postgres

- **What**: PostgreSQL powered by Neon, integrated into Vercel
- **Free tier**: Yes (same engine as Neon)
- **Pros**:
  - Tight Vercel integration, auto-creates preview branches per PR
- **Cons**:
  - More expensive than using Neon directly
  - No performance difference from Neon
  - Vendor lock-in to Vercel's pricing
- **Verdict**: Just use Neon directly. Same product, better pricing.

### Supabase

- **What**: Open-source Firebase alternative (PostgreSQL + auth + storage + realtime)
- **Free tier**: 500 MB database, 1 GB file storage, 50K monthly active users
- **Pros**:
  - All-in-one: database + auth + storage + realtime subscriptions
  - Row Level Security (RLS) built in
  - Dashboard with SQL editor
  - You already know it (StudyFlow, ArtistWay Helper)
- **Cons**:
  - Free tier pauses after 1 week of inactivity
  - Heavier than needed if you just want a database
  - Can get expensive at scale
- **Best for**: Rapid prototyping, all-in-one needs

---

## Auth Options

### Better Auth — RECOMMENDED for this project

- **What**: Open-source, framework-agnostic auth library
- **Cost**: Free / open source
- **Pros**:
  - Easy setup compared to Auth.js
  - No vendor lock-in
  - Full data ownership
  - Modern DX, TypeScript-first
  - Growing community momentum in 2025-2026
- **Cons**:
  - Newer, smaller ecosystem than NextAuth
  - Fewer pre-built UI components
- **Best for**: Projects that want control without the complexity of Auth.js

### NextAuth.js / Auth.js

- **What**: Open-source auth for Next.js (Auth.js is the framework-agnostic evolution)
- **Cost**: Free / open source
- **Pros**:
  - Most popular, largest ecosystem
  - Works with any database (Prisma, Drizzle adapters)
  - Full data ownership and control
  - Supports many providers (Google, GitHub, email, credentials)
- **Cons**:
  - Steep learning curve, especially for credentials auth
  - Documentation is frequently confusing
  - Complex configuration, especially non-standard flows
  - Breaking changes between versions
- **Best for**: Teams that want maximum flexibility and can invest in setup

### Clerk

- **What**: Managed auth + user management platform
- **Cost**: Free up to 10K MAU, then $0.02/MAU
- **Pros**:
  - Fastest setup by far (minutes, not hours)
  - Beautiful pre-built UI components (SignIn, UserButton, etc.)
  - Purpose-built for Next.js App Router
  - MFA, email verification, social logins out of the box
- **Cons**:
  - Vendor lock-in (your user data lives on Clerk's servers)
  - Can get expensive ($100+/mo for MFA features)
  - Reported reliability issues (random logouts)
  - Limited customization for complex flows
- **Best for**: Fast prototyping, teams that prioritize speed over control

---

## ORM Options

### Drizzle ORM — RECOMMENDED

- **Pros**:
  - TypeScript-first, code-first schema definition
  - Tiny bundle (~7.4kb), zero cold start overhead
  - SQL-like query builder = you know exactly what SQL runs
  - Best choice for serverless/edge (Vercel Functions)
  - Strong Turso, Neon, PlanetScale support
  - Up to 14x lower latency than ORMs with N+1 problems
- **Cons**:
  - Migrations require manual validation
  - Less "magic" than Prisma (you need to know some SQL)

### Prisma

- **Pros**:
  - Easier learning curve, great for teams new to databases
  - Prisma Migrate is gold standard for ease
  - Schema-first approach with `.prisma` file
  - Prisma 7 (late 2025) removed Rust engine = pure TypeScript now
  - Better for complex relations and nested queries
- **Cons**:
  - Larger bundle than Drizzle (though improved with v7)
  - Can generate hidden N+1 queries
  - `.prisma` schema is a separate DSL to learn

---

## Recommended Stack

For this project (solo developer, Next.js on Vercel, free tier, learning experience):

| Layer | Choice | Why |
|-------|--------|-----|
| **Database** | **Neon** (PostgreSQL) | Full Postgres, free tier, great DX, you learn a real production database |
| **ORM** | **Drizzle** | Lightweight, fast, TypeScript-native, teaches you SQL, perfect for Vercel |
| **Auth** | **Better Auth** or **Clerk** | Better Auth if you want to learn auth deeply; Clerk if you want to skip auth and focus on the music features |

**Note on Anthropic/Claude recommendations**: No specific database or auth partnerships found. Claude works with anything that sends it structured data — the stack choice is yours.

---

## Sources

- [Neon vs Turso for Solo Developers](https://solodevstack.com/blog/neon-vs-turso-solo-developers)
- [6 Best Serverless SQL Databases (2026)](https://www.devtoolsacademy.com/blog/serverless-sql-databases/)
- [Auth.js vs BetterAuth Comparison](https://www.wisp.blog/blog/authjs-vs-betterauth-for-nextjs-a-comprehensive-comparison)
- [NextAuth vs Clerk vs Auth.js (2025)](https://chhimpashubham.medium.com/nextauth-js-vs-clerk-vs-auth-js-which-is-best-for-your-next-js-app-in-2025-fc715c2ccbfd)
- [Drizzle vs Prisma (2026)](https://makerkit.dev/blog/tutorials/drizzle-vs-prisma)
- [Prisma vs Drizzle (DesignRevision)](https://designrevision.com/blog/prisma-vs-drizzle)
