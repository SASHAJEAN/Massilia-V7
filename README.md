# 🌊 Massilia — Pas fâché avec le plaisir

> AI-powered food & lifestyle discovery app for Marseille

Massilia helps you discover the best pastis bars, panisse spots, sunset apéros, and hidden Marseillais gems — powered by AI recommendations tailored to your mood, budget, and vibe.

---

## ✨ Features

- **AI Concierge** — Describe your mood in natural language, get hyperlocal recommendations
- **Mood-based discovery** — Chill / Party / Romantic / Family / Solo filters
- **Budget-aware** — Built for students and budget-conscious locals (€ → €€€)
- **Explore map** — Browse by category: pastis, panisse, sunset, beach, music
- **Community** — Reviews, photos, saved lists, social following
- **Gamification** — Earn badges (Pastis Pro, Sunset Chaser, Explorer...)
- **Personalized profile** — Budget, vibe, music preferences saved

---

## 🚀 Getting Started

### Prerequisites

- Node.js 16+
- npm or yarn

### Installation

```bash
git clone https://github.com/YOUR_USERNAME/massilia-app.git
cd massilia-app
npm install
npm start
```

Open [http://localhost:3000](http://localhost:3000) to view the app.

---

## 🗂️ Project Structure

```
massilia/
├── public/
│   └── index.html
├── src/
│   ├── components/          # Reusable UI components
│   │   ├── BottomNav.jsx
│   │   ├── MoodChip.jsx
│   │   ├── PlaceCard.jsx
│   │   └── AIConcierge.jsx
│   ├── screens/             # Full app screens
│   │   ├── OnboardingScreen.jsx
│   │   ├── HomeScreen.jsx
│   │   ├── AIScreen.jsx
│   │   ├── ExploreScreen.jsx
│   │   └── ProfileScreen.jsx
│   ├── data/
│   │   └── places.js        # Mock data (replace with Supabase)
│   ├── hooks/
│   │   └── useAI.js         # Claude API hook
│   ├── styles/
│   │   └── theme.js         # Design tokens
│   ├── App.jsx
│   └── index.js
└── package.json
```

---

## 🎨 Design System

| Token | Value |
|-------|-------|
| Primary Blue | `#29B6F6` |
| Accent Yellow | `#F5B800` |
| Background Beige | `#FDF6EC` |
| Dark | `#1A1A2E` |
| Coral | `#E8704A` |

---

## 🤖 AI Integration

The AI Concierge uses the **Anthropic Claude API**. To enable it:

1. Get an API key at [anthropic.com](https://console.anthropic.com)
2. Create a `.env` file in the project root:

```env
REACT_APP_ANTHROPIC_API_KEY=your_key_here
```

> ⚠️ For production, proxy API calls through a backend (e.g. Supabase Edge Functions) — never expose API keys in the frontend.

---

## 🗄️ Database (Supabase)

### Suggested schema

```sql
-- Places
create table places (
  id uuid primary key default gen_random_uuid(),
  name text not null,
  category text,           -- pastis | panisse | sunset | beach | music
  district text,
  price_level int,         -- 1 | 2 | 3
  rating numeric,
  lat numeric,
  lng numeric,
  description text,
  tags text[],
  created_at timestamptz default now()
);

-- Users
create table profiles (
  id uuid primary key references auth.users,
  username text unique,
  avatar_url text,
  budget_pref int default 2,
  vibe_pref text,
  music_pref text,
  badges text[],
  created_at timestamptz default now()
);

-- Reviews
create table reviews (
  id uuid primary key default gen_random_uuid(),
  place_id uuid references places,
  user_id uuid references profiles,
  rating int,
  body text,
  photo_url text,
  created_at timestamptz default now()
);

-- Saved spots
create table saved_places (
  user_id uuid references profiles,
  place_id uuid references places,
  primary key (user_id, place_id)
);
```

---

## 📱 Tech Stack

| Layer | Tech |
|-------|------|
| Frontend | React 18 + CSS Modules |
| Backend | Supabase (Auth, DB, Storage) |
| AI | Anthropic Claude API |
| Maps | Mapbox GL JS |
| Hosting | Vercel / Netlify |

---

## 🗺️ Roadmap

- [ ] Connect Supabase backend
- [ ] Add Mapbox map integration
- [ ] Real AI recommendations via Claude API
- [ ] User authentication (Google + email)
- [ ] Push notifications for trending spots
- [ ] React Native mobile version

---

## 📄 License

MIT — built with ☀️ in Marseille
