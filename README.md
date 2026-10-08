# Hush

Anonymous chat rooms built with Next.js (App Router). No accounts: each visitor gets a random name stored in their browser.

## Run it

```bash
npm install
npm run dev
```

Open http://localhost:3000 in two browser windows and talk to yourself.

## How it works

- `lib/store.js` keeps the last 200 messages per room in memory and notifies subscribers.
- `app/api/rooms/[room]/messages` returns history (GET) and accepts new messages (POST, 500 chars max, 1 per second per IP).
- `app/api/rooms/[room]/stream` is a Server-Sent Events stream, so new messages appear instantly.
- `components/Chat.js` joins a room, loads history, then listens to the stream.

## Before you deploy

The in-memory store works with `npm run dev` or `npm run build && npm start` on a single server. It will not work on serverless hosts (Vercel, Netlify), where each request may run on a different instance and memory is wiped. For those, replace `lib/store.js` with a database that has realtime, for example Supabase (Postgres + Realtime) or Upstash Redis pub/sub.

Also add before going public: profanity and spam filtering, a report/ban flow, and a stricter rate limit. Anonymous rooms attract abuse quickly.
# Hush
