# Flightwatch Proxy

Minimal Express proxy that forwards requests from the Flightwatch dashboard to the Anthropic API, handling CORS and keeping your API key secure.

## Deploy to Render (free)

1. Push this folder to a GitHub repo
2. Go to [render.com](https://render.com) → New → Web Service
3. Connect your GitHub repo
4. Set these options:
   - **Build command:** `npm install`
   - **Start command:** `npm start`
5. Add environment variable:
   - `ANTHROPIC_API_KEY` = your Anthropic API key (get one at console.anthropic.com)
6. Click **Deploy** — you'll get a URL like `https://flightwatch-proxy.onrender.com`

## Update your dashboard

In `index.html`, replace the fetch URL:

```js
// Before (calls Anthropic directly — blocked by CORS)
const response = await fetch("https://api.anthropic.com/v1/messages", { ... });

// After (calls your proxy)
const response = await fetch("https://YOUR-PROXY-URL.onrender.com/api/chat", { ... });
```

## Local development

```bash
ANTHROPIC_API_KEY=your_key node server.js
```

Then point your dashboard at `http://localhost:3000/api/chat`.
