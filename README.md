# MIAS MDX — Web UI by 𝑷𝑹𝑬𝑪𝑰𝑬𝑶𝑼𝑺 x

> **WhatsApp Bot Web Interface** — Music Player + Session Generator

## Features
- 🎵 **Music Player** — plays songs directly via embedded YouTube, full clickable playlist
- 📱 **Session Pairing** — generate your WhatsApp SESSION_ID via QR code or pairing code
- 🌙 Dark purple neon design

## Deploy on Vercel (Fastest)
1. Push this folder to a GitHub repo
2. Go to https://vercel.com/new → Import repo
3. Build command: `npm run build`
4. Output directory: `dist`
5. Deploy ✅

## Local Development
```bash
npm install
npm run dev
# Open http://localhost:5173
```

## Deploy Anywhere
- **Netlify**: Run `npm run build` → drag `dist/` to netlify.com/drop
- **GitHub Pages**: Run `npm run build` → upload `dist/` contents
- **Railway / Render**: Connect repo, set build command `npm run build`, serve from `dist/`

## Connecting Your Real Bot Backend (Optional)
The Session Pairing tab will try to connect to `/session-ws` (WebSocket) on the same host.
If no backend is found, it runs in demo mode (still generates a sample SESSION_ID format).

To connect your real Baileys bot:
1. Add a WebSocket server at `/session-ws` to your bot's Express server
2. Send these messages to the frontend:
   - `{ type: "qr", qrUrl: "https://..." }` — show QR
   - `{ type: "pairing_code", code: "ABCD-EFGH" }` — show code
   - `{ type: "authenticated", sessionId: "base64..." }` — session done

## SESSION_ID Format (Baileys)
The session is a base64 of your Baileys auth folder JSON:
```js
// After pairing, encode your mias_mdx_auth folder:
const files = {};
fs.readdirSync("mias_mdx_auth").forEach(f => {
  files[f] = fs.readFileSync(`mias_mdx_auth/${f}`, "utf8");
});
const SESSION_ID = Buffer.from(JSON.stringify(files)).toString("base64");
```

Made with ❤️ by 𝑷𝑹𝑬𝑪𝑰𝑶𝑼𝑺 x
