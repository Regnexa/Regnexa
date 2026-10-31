# Regnexa V1

A bilingual, public-access governance, risk and compliance website with a server-side OpenAI Responses API endpoint and official-domain web search.

## Included
- `index.html`: responsive English/Arabic website and embedded chat interface.
- `api/chat.js`: Vercel serverless endpoint. Keeps the OpenAI API key on the server, restricts web search to an allowlist of official regulatory/government/standard-setter domains, returns source citations, and applies a daily per-IP limit.
- `vercel.json`: Vercel function configuration.
- `.env.example`: required and optional environment variables.

## Deploy to Vercel
1. Upload this folder to a GitHub repository, or import the repository into Vercel.
2. In Vercel, create a new project and select the repository. No build command is required; the site is static HTML plus a serverless function.
3. In Project Settings → Environment Variables, add `OPENAI_API_KEY`. Optionally set `OPENAI_MODEL` and `DAILY_LIMIT`.
4. For reliable daily limits across serverless instances, create an Upstash Redis database and set `UPSTASH_REDIS_REST_URL` and `UPSTASH_REDIS_REST_TOKEN`.
5. Deploy. Test the site and `/api/chat` after deployment.

## Important setup notes
- OpenAI API billing is separate from a ChatGPT subscription. The API key and billing account must be supplied by the site owner.
- Do not expose `OPENAI_API_KEY` in browser code or commit real secrets to GitHub.
- Without Upstash, the endpoint uses an in-memory fallback limit. This is suitable only for preview/testing; it is not a reliable global daily limit in a serverless production deployment.
- Search is constrained to the official domains listed in `api/chat.js`. Add or remove domains only after validating that they are official primary sources.
- The public source directory in the homepage is a starting list of links, not a complete indexed legal database. Regulatory applicability and current effective dates must be verified against the official publication.
- This is an initial technical build, not a legal-compliance certification. Add privacy notice, terms, abuse controls, monitoring and a reviewed regulatory content process before public launch.

## Local preview
Open `index.html` directly to preview the static website. The AI endpoint requires deployment in a Node/Vercel-compatible environment and a valid server-side API key.
