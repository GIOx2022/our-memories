# 💕 Our Memories

> *A private digital memory book built with React, Vite, Tailwind CSS, and Supabase.*
>
> "Sebuah tempat kecil di internet yang hanya berisi cerita tentang kami."

Our Memories is a personal digital memory book designed to preserve special moments, photos, videos, stories, and meaningful experiences in one beautiful place.

---

## ✨ Features

- 📸 **Photo Memories** — Save and display individual photo memories.
- 🎥 **Video Memories** — Preserve special moments through videos.
- 📖 **Memory Stories** — Add personal stories and descriptions.
- 🗓️ **Relationship Timeline** — Document important moments in your journey together.
- 🖼️ **Photo Gallery** — Browse memories in a beautiful masonry layout.
- 💌 **Love Notes** — Store meaningful quotes and messages.
- 🔍 **Search & Filter** — Easily find memories by keyword and type.
- ☁️ **Cloud Storage** — Store photos and videos using Supabase Storage.
- 📱 **Responsive Design** — Accessible from desktop, tablet, and mobile devices.

---

## 🛠️ Tech Stack

- **React 18** + **Vite 4**
- **Tailwind CSS 3**
- **React Router 6**
- **Framer Motion 10**
- **Lucide React**
- **Supabase** — Database and Storage
- **Vercel** — Deployment

---

## 🚀 Getting Started

### 1. Clone the Repository

```bash
git clone https://github.com/GIOx2022/our-memories.git
cd our-memories
```

### 2. Install Dependencies

```bash
npm install
```

### 3. Setup Environment Variables

Copy `.env.example` to `.env.local`:

```bash
cp .env.example .env.local
```

Add your Supabase project credentials:

```env
VITE_SUPABASE_URL=https://your-project.supabase.co
VITE_SUPABASE_ANON_KEY=your-publishable-key-here
```

> ⚠️ Never commit your real environment variables or Supabase secret keys to GitHub. Only use the Publishable Key in the frontend.

### 4. Setup Supabase Database

1. Open the [Supabase Dashboard](https://supabase.com/dashboard).
2. Select your project.
3. Navigate to **SQL Editor**.
4. Run the contents of `supabase-schema.sql`.

The schema creates the following tables:

- `memories` — Individual memories.
- `memory_images` — Additional media associated with memories.
- `quotes` — Love notes and quotes.
- `timeline` — Important relationship events.

It also configures:

- Row Level Security (RLS).
- Public read policies.
- Authenticated write policies.
- Database indexes.

**Important:** Public database access requires both the appropriate SQL `GRANT` privileges and RLS policies.

### 5. Setup Supabase Storage

1. Open **Storage** in your Supabase Dashboard.
2. Create a bucket named `memories`.
3. Set the bucket visibility to **Public**.
4. Upload your media using the following folder structure:

```text
memories/
├── photos/
│   ├── first-date.jpg
│   ├── vacation.jpg
│   └── anniversary.jpg
│
└── videos/
    ├── special-moment.mp4
    └── anniversary.mp4
```

Upload photos and videos to their respective folders and copy their public URLs into the database.

### 6. Run Development Server

```bash
npm run dev
```

Open your browser at:

http://localhost:5173

---

## 📄 Pages & Routes

| Route | Description |
|---|---|
| `/` | Homepage — Hero, Stats, and Featured Memories |
| `/memories` | All memories with search and filters |
| `/memories/:id` | Memory detail with gallery and video |
| `/timeline` | Relationship journey timeline |
| `/gallery` | Masonry photo gallery with lightbox |
| `/videos` | Video memories |
| `/notes` | Love notes and quotes |

---

## 💖 Adding Memories

This application does not require public user authentication.

Memories are managed directly through the Supabase Dashboard.

### Memory Management

1. Open **Supabase Dashboard → Storage**.
2. Upload your photo or video.
3. Copy the file's public URL.
4. Open **Table Editor → memories**.
5. Insert a new row with the media information.

### Memory Types

Each photo or video is stored as an individual memory.

| Type | Description |
|---|---|
| `photo` | An individual photo memory |
| `video` | An individual video memory |
| `story` | A text-based memory or personal story |

### Example: Adding a Photo

| Column | Example |
|---|---|
| `title` | Our First Date |
| `slug` | our-first-date |
| `description` | The beginning of our story |
| `location` | Bandung |
| `memory_date` | 2025-06-17 |
| `type` | photo |
| `cover_image` | Public photo URL |
| `video_url` | NULL |
| `is_featured` | true |

### Example: Adding a Video

| Column | Example |
|---|---|
| `title` | Our Anniversary |
| `slug` | our-anniversary |
| `description` | A special moment together |
| `location` | Jakarta |
| `memory_date` | 2026-06-17 |
| `type` | video |
| `cover_image` | Optional thumbnail URL |
| `video_url` | Public video URL |
| `is_featured` | false |

### Supabase Storage Public URL Format

Photos:

```text
https://[project].supabase.co/storage/v1/object/public/memories/photos/filename.jpg
```

Videos:

```text
https://[project].supabase.co/storage/v1/object/public/memories/videos/filename.mp4
```

---

## 🌐 Deployment to Vercel

Deploy your website so it can be accessed from anywhere, including mobile devices.

1. Push your project to GitHub.
2. Open [Vercel](https://vercel.com).
3. Import your GitHub repository.
4. Configure the environment variables:

```env
VITE_SUPABASE_URL=https://your-project.supabase.co
VITE_SUPABASE_ANON_KEY=your-publishable-key-here
```

5. Click **Deploy**.

The `vercel.json` configuration handles React Router rewrites automatically.

Once deployment is complete, your website will have a public URL.

---

## 🔐 Security Notes

- ✅ Anonymous visitors can read public memories.
- ✅ Row Level Security (RLS) protects database access.
- ✅ Public visitors cannot insert, update, or delete database records.
- ✅ Only Supabase Publishable Keys are used in frontend code.
- ✅ Secret keys and service role keys must never be exposed in the browser.
- ✅ Storage uploads and database management are handled through the Supabase Dashboard.
- ⚠️ Public Storage buckets allow anyone with the public file URL to access stored media.

**Privacy Notice:** Although the website is intended as a personal memory book, public database policies and a public Storage bucket mean that its content is not private or restricted to your partner. Do not upload sensitive or confidential media.

---

## 🌱 Without Supabase

The application can use seed data when Supabase credentials are not configured, making it useful for local development and preview.

---

## 📁 Project Structure

```text
src/
├── components/          # Reusable UI components
│   ├── Navbar.jsx
│   ├── Footer.jsx
│   ├── MemoryCard.jsx
│   ├── TimelineItem.jsx
│   ├── ImageLightbox.jsx
│   ├── QuoteCard.jsx
│   ├── Skeleton.jsx
│   ├── EmptyState.jsx
│   └── ErrorState.jsx
│
├── pages/               # Application pages
│   ├── Home.jsx
│   ├── Memories.jsx
│   ├── MemoryDetail.jsx
│   ├── TimelinePage.jsx
│   ├── Gallery.jsx
│   ├── Videos.jsx
│   └── Notes.jsx
│
├── lib/
│   ├── supabase.js      # Supabase client
│   └── seedData.js      # Demo seed data
│
├── services/
│   └── memoryService.js # Data fetching
│
├── hooks/
│   └── useMemory.js     # Custom React hooks
│
├── App.jsx              # Routes and page transitions
├── main.jsx             # Application entry point
└── index.css            # Global styles and Tailwind
```

---

Made with ❤️

**Our Memories** — Every picture tells a story, every moment becomes a memory.