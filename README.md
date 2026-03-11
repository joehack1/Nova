# My Personal Assistant

A single-page, front-end–only AI companion that runs entirely in the browser. It chats, plans your day, keeps a journal, speaks aloud, listens to you, sends reminders, and lets you switch between multiple LLM providers without any backend services.

## Features
- Chat UI with typing indicator, memory extraction, and multi-provider fallback.
- Voice input (Web Speech API) and voice output via ElevenLabs or built-in browser voices.
- Day planner with dated task lists, categories, and quick AI-generated plans.
- Daily journal with AI reflection on saved entries.
- Mood tracker, reminders, toast notifications, and persistent state in `localStorage`.
- Theming system with five presets and quick reapply controls.

## Quick Start
- Install a modern desktop browser (Chrome/Edge recommended; Safari speech support varies).
- Start a local web server from the project root (avoids `file://` CORS blocks):
  - `python -m http.server 8000`
- Open `http://localhost:8000/my-assistant.html`.
- Complete the setup screen (your name, assistant name, primary model key).
- Open **Settings → API Keys** to paste credentials for any provider you plan to use.
- Allow microphone/notification permissions when prompted if you want voice or reminders.

## API Providers
The assistant can route requests to several providers; configure only the ones you need:
- Anthropic (primary setup key)
- BigModel (Zhipu), Gemini, Groq, Cerebras
- OpenRouter, GitHub Models, Public AI, Wisdom Gate, Mistral
- ElevenLabs for TTS (or switch to browser voices in Settings → Speech)

Credentials are stored locally in `localStorage` and used only in client-side `fetch` calls. Do not commit real keys to version control. If the starter file contains sample keys in `my-assistant.html`, replace them with blanks or your own values before publishing and rotate any previously exposed keys.

## Data & Privacy
- Local persistence: `pa_state` in `localStorage` keeps chat history, tasks, journal, mood, settings, and API keys.
- Clear everything via **Settings → Data → Clear All Data** or by clearing browser storage.
- Reminders use the browser Notification API; nothing is sent to external servers besides your chosen model/TTS endpoints.

## Project Layout
- `my-assistant.html` — markup, styling hooks, and all app logic (vanilla JS).
- `app.css` — theme tokens, layout, animations, and component styles.
There is no build step or external dependencies beyond browser APIs and the provider endpoints you configure.

## Development Tips
- Keep running through `http://localhost` to avoid blocked cross-origin requests.
- Most logic lives in the bottom `<script>` of `my-assistant.html`; theme tokens are centralized in `app.css`.
- When editing provider calls, ensure CORS is permitted by your chosen endpoint and that you pass the right auth headers.

## Deployment
- Host as static files on any HTTPS-capable server or CDN.
- For public deployments, strip any default/demo keys from `my-assistant.html` and rely on runtime entry via Settings.
- If you disable microphone or notifications in the browser, related features will gracefully degrade.

## Troubleshooting
- Seeing “failed to fetch” while on `file://`? Serve via `python -m http.server` (or any static server) instead.
- Speech recognition not working: ensure the browser supports `SpeechRecognition` and mic permission is granted.
- TTS silent: switch engines in Settings → Speech or confirm your ElevenLabs key/voice selection.
