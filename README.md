# 🎙️ ReVoice — AI Podcast Content Repurposing Engine

Turn one podcast episode into **two weeks of content** — automatically.

Upload an audio file → get a blog post, newsletter, X thread, IG carousels, Reels script, and quote graphics, all written in your voice.

---

## 🚀 Quick Start (Local Dev)

### 1. Clone / extract this project
```bash
cd revoice
```

### 2. Install dependencies
```bash
npm install
```

### 3. Configure environment variables
```bash
cp .env.example .env.local
```

Edit `.env.local` and add your API keys:
```
ANTHROPIC_API_KEY=sk-ant-...     # From console.anthropic.com
OPENAI_API_KEY=sk-...             # From platform.openai.com
NEXTAUTH_SECRET=any-random-string
NEXTAUTH_URL=http://localhost:3000
```

### 4. Run the dev server
```bash
npm run dev
```

Open [http://localhost:3000](http://localhost:3000)

---

## 🌐 Deploy to Vercel (Recommended — Free)

### Option A: Vercel CLI
```bash
npm i -g vercel
vercel
```

Follow prompts, then add environment variables in the Vercel dashboard.

### Option B: GitHub → Vercel
1. Push this repo to GitHub
2. Go to [vercel.com](https://vercel.com) → "New Project"
3. Import your GitHub repo
4. Add environment variables in Vercel project settings:
   - `ANTHROPIC_API_KEY`
   - `OPENAI_API_KEY`
   - `NEXTAUTH_SECRET`
   - `NEXTAUTH_URL` → set to your `.vercel.app` URL

### Important Vercel Settings
In your Vercel project → **Settings → Functions**:
- Set **Max Duration** to `120` seconds (needed for AI processing)

---

## 🏗️ Tech Stack

| Layer | Technology |
|---|---|
| Framework | Next.js 14 (App Router) |
| Language | TypeScript |
| Styling | Tailwind CSS + custom CSS |
| Transcription | OpenAI Whisper API |
| Content AI | Anthropic Claude (claude-opus-4-5) |
| Deployment | Vercel |

---

## 📁 Project Structure

```
revoice/
├── app/
│   ├── page.tsx              # Landing page
│   ├── upload/
│   │   └── page.tsx          # Upload + generation UI
│   ├── api/
│   │   ├── transcribe/
│   │   │   └── route.ts      # Whisper transcription endpoint
│   │   └── generate/
│   │       └── route.ts      # Claude content generation endpoint
│   ├── globals.css           # Global styles + design tokens
│   └── layout.tsx            # Root layout + metadata
├── components/
│   └── OutputView.tsx        # 6-tab content output viewer
├── .env.example              # Environment variable template
├── next.config.js
├── tailwind.config.js
└── package.json
```

---

## 🎯 Features

### Core
- **Audio/Video Upload** — drag & drop any MP3, WAV, MP4, M4A, OGG, WEBM
- **Whisper Transcription** — accurate transcription via OpenAI Whisper API
- **Manual Text Input** — paste transcript directly (no audio needed)
- **AI Content Generation** — Claude generates all 6 formats in one pass

### 6 Content Formats
1. **SEO Blog Post** — 800-1200 word article with H1/H2 structure
2. **X/Twitter Thread** — 12-post viral thread with strong hook
3. **Newsletter** — Conversational edition with subject line
4. **Instagram Carousels** — 2 carousels with slide-by-slide copy
5. **Reels Script** — 60-90 second script with timestamps
6. **Quote Graphics** — 8 pull-quotes, styled in 3 visual formats

### UX
- Real-time progress indicator with stage tracking
- Copy to clipboard per format
- Download individual format as .txt
- Download full content pack as single .txt file
- Responsive design

---

## 💰 Estimated API Costs

Per episode (45-60 min podcast):
- **Whisper transcription**: ~$0.30–$0.60
- **Claude generation**: ~$0.10–$0.20
- **Total per episode**: ~$0.40–$0.80

At $29/month Pro (20 uploads/month), your API costs ~$8–16/month → **healthy margins**.

---

## 🔧 Customization

### Change the AI Model
In `app/api/generate/route.ts`, update the model:
```ts
model: 'claude-opus-4-5',  // Current: most capable
// model: 'claude-sonnet-4-5',  // Faster + cheaper
```

### Adjust Content Length
Edit the prompts in `app/api/generate/route.ts` in the `USER_PROMPT` function.

### Add Authentication
The project includes `next-auth` as a dependency. See the [NextAuth docs](https://next-auth.js.org) to set up Google/GitHub OAuth using your `.env.local` credentials.

### Add a Database
To persist generated content, add:
- [Supabase](https://supabase.com) (PostgreSQL, free tier)
- [Prisma](https://prisma.io) (ORM)

---

## 🐛 Troubleshooting

**"ANTHROPIC_API_KEY is not configured"**
→ Make sure your `.env.local` file exists and has the correct key name.

**"File too large"**
→ Whisper has a 25MB limit. Compress audio to MP3 128kbps or trim the episode.

**"Failed to parse AI response"**
→ Rare edge case. Click "New Upload" and try again — Claude sometimes returns malformed JSON.

**Slow processing**
→ 45-60min podcasts take 2-4 minutes. This is normal — Whisper + Claude generation takes time.

---

## 📈 Roadmap (Future Features)

- [ ] User accounts + history dashboard
- [ ] Stripe billing integration
- [ ] Voice profile learning (analyze past episodes for tone)
- [ ] Content calendar view (schedule 14 days of posts)
- [ ] Direct publishing to Buffer/Typefully/Beehiiv
- [ ] YouTube video support
- [ ] Multi-language support

---

## 📄 License

MIT — free to use, modify, and deploy commercially.
