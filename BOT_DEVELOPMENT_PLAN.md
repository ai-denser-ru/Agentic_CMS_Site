# Agentic CMS Bot: Development & Operations Plan (v1.1.0)

This document defines the core logic, orchestration rules, and deployment safety standards for the Telegram bot managing the Agentic CMS.

## 🚀 Core Mission
The bot acts as a **reliable orchestrator** for content management, ensuring that any human request is translated into a stable, verified, and multi-locale synchronized update.

---

## 🛠 Orchestration Rules (Internal Logic)

### 1. Mandatory Preview (Rule #1)
- **Workflow:** `Edit -> /preview -> Verify -> /publish`.
- **Constraint:** The bot is strictly forbidden from suggesting `/publish` until a successful `/preview` URL has been generated and shared with the user.
- **Goal:** Prevent broken builds or typos from reaching the production branch.

### 2. Full Locale Parity (Rule #2)
- **Locales:** RU, EN, ES, PT-BR.
- **Process:** Whenever a global setting (like `site_name`) is updated, the bot MUST sequentially update all 4 locales.
- **Reporting:** The bot must provide status updates for each language update ("RU updated, moving to EN...").

### 3. Read-Modify-Write (Data Integrity)
- **Constraint:** Settings tools (`get_settings` and `update_settings`) must always perform a full read before a merge/update.
- **Technical Fields:** Never overwrite fields like `id`, `site`, or `base` unless explicitly requested.

### 4. Safety & Rollback (Rule #3)
- **Proactive Undo:** Whenever a `/preview` link is issued, the bot must offer `/rollback` as a primary option alongside `/publish`.
- **Immediate Reversion:** If the user expresses concern or rejects a preview, call `rollback_changes` immediately.

---

## 📡 Communication Protocol

### 1. HTML-Based Messaging
- All bot responses use `ParseMode: "HTML"`.
- All dynamic data (MCP results, JSON) MUST be wrapped in `<pre>` tags and sanitized via `escapeHTML` to prevent `400 Bad Request` errors caused by special characters.

### 2. Proactive Footers
Tool execution must always be followed by a "Next Steps" footer to guide the user:
- **After Update:** "🧪 Changes applied locally. Run /preview to check."
- **After Preview:** "👉 Link: [URL]\nIf good: /publish\nIf bad: /rollback"

---

## 🌍 Site & Deployment Specs

- **Technology:** Astro 5 (Static Site Generation).
- **GitHub Pages:** `ai-denser-ru.github.io/Agentic_CMS_Site/`.
- **Preview Engine:** `npm run preview` + `localtunnel` (port 4321).
- **Base URL:** All preview links MUST include the `/Agentic_CMS_Site/` subpath.

---

## 📋 Ongoing Tasks
- [x] Stabilize `Markdown` to `HTML` migration.
- [x] Implement the `base` path injection for previews.
- [x] Hardcode the "Next Steps" proactivity footers.
- [ ] Implement multi-language AI translation within the `update_settings` reasoning chain.
- [ ] Add automated build verification after every `git_push`.

---
*Created on: 2026-03-28 by Antigravity AI.*
