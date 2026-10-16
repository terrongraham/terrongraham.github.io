# Cloudflare Worker AI Proxy for Terron Graham's Portfolio

This worker acts as a secure, rate-limited proxy between the frontend chat widget and Google's Gemini 2.5 Flash API.

## Features
- **Secret Protection:** \GEMINI_API_KEY\ is kept strictly on Cloudflare's serverless edge.
- **CORS Restricted:** Only permits requests from \https://terrongraham.com\, \https://terrongraham.github.io\, and local development.
- **IP-Based Rate Limiting:** Enforces max 5 questions per minute per client IP.
- **Strict Grounding:** Injects Terron's verified resume and project accomplishments so the model answers accurately without hallucinating.

---

## 2-Minute Deployment Options

### Option A: Using the Cloudflare Dashboard (No CLI needed)
1. Go to [dash.cloudflare.com](https://dash.cloudflare.com/) and sign up / log in (100% Free).
2. Click **Compute (Workers) > Workers & Pages > Create application > Create Worker**.
3. Name it \	erron-portfolio-ai\ and click **Deploy**.
4. Click **Edit Code** and paste the entire contents of \worker.js\ into the editor, then click **Deploy**.
5. Go to **Settings > Variables and Secrets > Add**:
   - Variable name: \GEMINI_API_KEY\
   - Value: *(Your Google AI Studio Gemini API Key)*
   - Click **Encrypt** and **Save**.
6. Copy your Worker URL (e.g. \https://terron-portfolio-ai.<your-subdomain>.workers.dev\).
7. Paste this URL into \index.html\ inside the \PORTFOLIO_AI_CONFIG.API_URL\ setting!

### Option B: Using Wrangler CLI
\\\ash
cd api-proxy
npx wrangler login
npx wrangler secret put GEMINI_API_KEY
npx wrangler deploy
\\\
