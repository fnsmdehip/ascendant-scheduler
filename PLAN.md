# Implementation Plan

## A. Fork & Customize Postiz
1. **Clone & Bootstrap**
   ```bash
   git clone https://github.com/gitroomhq/postiz-app.git
   cd postiz-app
   npm install
   cp .env.example .env  # fill in YOUR_DB_URL, JWT_SECRET, etc.
   npm run dev
   ```
2. **Configure API Keys**
   - Add OAuth credentials for each platform in `.env`.
3. **Schedule & Queue**
   - Edit job runner config (`/server/jobs/...`) to adjust posting schedules and retries.
4. **Thumbnail Microservice**
   - Add `/api/thumbnail` route for AI image generation using OpenAI Images API.
5. **UI in Cursor IDE**
   - Use React/Tailwind templates to integrate thumbnail generator and restyle pages.

## B. DIY Minimal Stack in Cursor

1. **Project Setup**
   ```bash
   npx create-next-app ascendant-scheduler
   cd ascendant-scheduler
   npm install tailwindcss @prisma/client next-auth bullmq
   ```
2. **Database & ORM**
   - Prisma + PostgreSQL (Supabase).
   - Model `User`, `SocialAccount`, `Post`, `ScheduleJob`.
3. **Authentication**
   - NextAuth with email/password + OAuth.
4. **API Integrations**
   - Service modules in `/lib/apis/{platform}.ts` for each social network.
5. **Scheduling Engine**
   - BullMQ with Redis (Upstash).
   - Enqueue jobs at scheduled times; workers publish posts.
6. **Thumbnail Service**
   - `/pages/api/thumbnail.ts` to call OpenAI Images API based on user prompt.
7. **Scheduler UI**
   - Use shadcn/ui in Cursor IDE for a calendar/list view and post form.
8. **Deployment**
   - Vercel for Next.js, Upstash for Redis, Supabase for PostgreSQL.

## Next Steps
1. Decide approach: **Fork Postiz** or **DIY in Cursor**.
2. Clone this scaffold in Cursor IDE.
3. Implement first social API integration (e.g., X/Twitter).
4. Build and test the thumbnail endpoint.
5. Iterate across additional platforms and features.
