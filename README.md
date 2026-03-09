# 🧠 AI Notes — Interview Prep & LLM Debate Arena

A single-file, zero-dependency progressive web app that lives in one `.html` file. It gives you two deeply specialised AI tools — a FAANG interview preparation assistant and a multi-LLM debate engine — wrapped inside a mobile-first Notes interface.

**No server. No build step. No login. Open the file in any browser and go.**

---

## ✨ Features at a Glance

| Feature | Description |
|---|---|
| 🤖 Multi-provider LLM | Anthropic Claude, OpenAI GPT, Google Gemini, Groq/Llama |
| ☕ Coding Interview Prep | Java solutions with complexity, walkthrough, gotchas, Q&A |
| 🏗️ System Design Prep | Full Hello Interview / Evan King framework with diagrams |
| ⚔️ LLM Debate Arena | Fan-out → cross-critique → judge synthesis across all AIs |
| 🎯 10 Expert Domains | Finance, Medical, Legal, Career, Nutrition, Tech, Business… |
| 🎤 Voice Input | Web Speech API — speak your question |
| 📡 True Streaming | Real-time skeleton UI fills as tokens arrive |
| 🔑 Inline Key Management | Add API keys directly on provider cards — no settings page |
| 💾 Local-only Storage | Keys never leave your browser |

---

## 🚀 Quick Start

1. Download `notes-final.html`
2. Open in any modern browser (Chrome / Edge / Safari recommended)
3. Tap **⚔️ LLM Debate Arena** or **☕ Java Coding** or **🏗️ System Design**
4. Tap the **🔑** icon on any provider card to add your API key
5. Ask your question

That's it. No npm install. No server. No account.

---

## 📱 Screenshots / Flow

```
Home (Notes list)
├── ☕ Quick Ref – Java          → Coding Interview Tool
├── 🏗️ Quick Ref – System Design → System Design Tool  
└── ⚔️ LLM Debate Arena          → Multi-LLM Debate Engine
```

---

## 🛠️ Tech Stack

| Layer | Technology |
|---|---|
| **Runtime** | Vanilla HTML5 + CSS3 + JavaScript (ES2020) — zero frameworks |
| **Styling** | Pure CSS with CSS custom properties (variables), flexbox, grid |
| **Animations** | CSS keyframe animations (skeleton shimmer, mic pulse, waveform) |
| **AI APIs** | Fetch API with `ReadableStream` for SSE streaming |
| **Voice** | Web Speech API (`webkitSpeechRecognition`) |
| **Storage** | `localStorage` with in-memory `_memKeys` fallback for sandboxed iframes |
| **Fonts** | System font stack (`-apple-system`, `sans-serif`) — no web fonts |

### LLM Providers Supported

| Provider | Models | API Endpoint |
|---|---|---|
| **Anthropic** | Claude Sonnet 4.5, Opus 4.5, Haiku 4.5 | `api.anthropic.com/v1/messages` |
| **OpenAI** | GPT-4o, GPT-4o mini, o1-mini | `api.openai.com/v1/chat/completions` |
| **Google Gemini** | Gemini 2.0 Flash, 1.5 Pro, 1.5 Flash | `generativelanguage.googleapis.com/v1beta` |
| **Groq** | Llama 3.3 70B, Mixtral 8x7B, Llama 3 70B | `api.groq.com/openai/v1/chat/completions` |

---

## 🎯 Tool 1 — Coding Interview Prep

Type or speak a coding problem. The AI responds as an elite Java coding coach.

**Output structure (6 tabs):**

1. **Overview** — One-line summary, time/space complexity with explanation, algorithm pattern, first-person thought process, real-world analogy
2. **Code** — Complete, well-commented Java solution with syntax highlighting
3. **Walkthrough** — Step-by-step breakdown with variable names and reasoning
4. **Gotchas** — Edge cases and tricky parts with exact handling
5. **Q&A** — 5 realistic follow-up questions with confident answers
6. **Alternatives** — 3 alternative approaches with complexity and trade-off verdict

**Depth modes:** Interview Ready · Deep Walkthrough · Explain Like I'm New

---

## 🏗️ Tool 2 — System Design Prep (Hello Interview Framework)

Based on Evan King's Hello Interview methodology used at FAANG companies.

**Output structure (4 main tabs, 5 sub-tabs in Walkthrough):**

```
Overview
├── Problem statement
├── Clarifying questions
├── Functional requirements
├── Non-functional requirements  
├── Out of scope
├── Capacity estimation (QPS, storage, plain-English story)
└── Interview framing (speak guide)

Design Walkthrough
├── Core Entities     — domain nouns only, no fields yet
├── API Design        — endpoints + protocol choice (REST/gRPC/GraphQL) + real-time layer
├── HLD Walkthrough   — FR-by-FR: draw diagram one requirement at a time
├── Scaled Design     — Diagram 1 (baseline) → Diagram 2 (evolved, ★ markers for NFRs)
└── Schema            — per-table: storage choice + key fields + indexes + access pattern

Deep Dives
└── Per NFR: Bad → Good → Great progression with numbers

Q&A
└── Follow-up questions with answers
```

**Streaming skeleton UI:** 7 named slots fill progressively as tokens arrive (CQ at ~1s, requirements at ~2-3s, capacity at ~4-5s).

---

## ⚔️ Tool 3 — LLM Debate Arena

The centrepiece feature. Ask any question and watch multiple AIs debate to a synthesised best answer.

### Architecture: 3-Phase Debate

```
Phase 1 ─ Fan-Out (parallel)
  All selected LLMs receive identical prompt simultaneously
  Each answers independently — genuine diversity, no echo
  
Phase 2 ─ Cross-Critique (sequential rounds)
  Each LLM sees all other answers
  Must: acknowledge what others got right, challenge specific claims,
        identify gaps, state what it would revise
  
Phase 3 ─ Synthesis (judge call)
  Orchestrator reads all answers + all critiques
  Produces final answer better than any individual
  Cites which model contributed what
```

### Judge Modes

| Mode | How It Works |
|---|---|
| 🏆 **Strongest model** | Highest-ranked available model judges and synthesises |
| 🗳️ **Majority vote** | Each AI votes for the best answer (fuzzy name matching); winner's answer shown |
| 🧠 **Meta-synthesis** | Dedicated orchestrator call with explicit attribution per insight |

### Domain Expert Engine

Auto-detects domain from question keywords, or pick manually:

| Domain | Expert Role |
|---|---|
| 💰 Finance & Investing | CFA + SEBI-registered investment advisor |
| 🏦 Loans & Credit | Senior banking professional + credit counsellor |
| 🩺 Health & Medicine | Consultant physician, MD, 20yr clinical experience |
| ⚖️ Legal & Rights | Senior advocate, civil/criminal/corporate law |
| 🚀 Career & Jobs | Executive coach + ex-FAANG recruiter |
| 🥗 Fitness & Nutrition | Registered dietitian + certified personal trainer |
| 💻 Software & Tech | Principal engineer + architect |
| 🏗️ System Design | Evan King Hello Interview framework |
| 📊 Business & Strategy | Ex-McKinsey consultant + serial entrepreneur |
| 🌐 General | World-class polymath |

For System Design questions, the judge uses the full `sdPrompt()` and renders the complete tabbed SD template — same output as Tool 2.

### Inline Key Management

Each provider card has a 🔑 button. Tap to expand an inline key panel:
- Shows provider-specific hint (where to get the key)
- Password input pre-filled with saved key
- Save / Clear buttons
- Keys shared with main Settings — one store, two views
- `localStorage` with `_memKeys` in-memory fallback for sandboxed environments

---

## 🏛️ Architecture

### Single-File Design

Everything lives in one `.html` file:

```
notes-final.html  (~145KB, ~1900 JS lines)
├── <style>     — ~247 CSS rules, ~23KB
├── <body>      — 4 panels (list, tool, debate)  
└── <script>    — ~1900 lines vanilla JS
    ├── State & constants
    ├── Provider configs (PROVIDERS, DB_PROVIDERS)
    ├── Navigation (openTool, goBack, openDebate, closeDebate)
    ├── Voice input (startMic, stopMic, SpeechRecognition)
    ├── Streaming engine (generate, patch, showSkeleton)
    ├── Prompt builders (codingPrompt, sdPrompt)
    ├── Renderers (renderCoding, renderSD)
    ├── Domain engine (DB_DOMAINS, resolvedDomain, buildExpertPrompt…)
    ├── Debate orchestrator (runDebate, 3 phases, parseVote)
    └── Init
```

### Streaming Pipeline

```
fetch(url, { body: JSON.stringify({stream: true}) })
  → res.body.getReader()          ReadableStream
  → TextDecoder (flush: true)     UTF-8 decode
  → line-by-line SSE parser       data: {...}
  → JSON.parse(delta)             per-provider extractDelta()
  → accumulate full text (c)
  → patch(c, dk)                  progressive skeleton fill
  → on complete → renderSD/renderCoding(parsed)
```

**Provider-specific delta extraction:**
- Anthropic: `content_block_delta.delta.text`
- OpenAI / Groq: `choices[0].delta.content`
- Gemini: SSE via `alt=sse`, `candidates[0].content.parts[0].text`

### JSON Parse Strategy (multi-attempt)

```javascript
1. Direct JSON.parse(c)                       // happy path
2. Extract {…} by bracket scan               // leading/trailing garbage
3. Trailing-comma repair + JSON.parse         // common LLM artifact
4. Progressive partial — render what arrived  // timeout fallback
```

### Sandboxed iframe Compatibility

Deployed inside `claude.ai` which sandboxes iframes:
- `localStorage` wrapped in try/catch everywhere
- `_memKeys{}` in-memory object as fallback
- No `document.cookie`, no `window.opener`, no cross-origin reads
- All API calls use `anthropic-dangerous-direct-browser-access: true` header for Anthropic

---

## 📁 File Structure

```
notes-final.html     Single deployable file — open directly in browser
README.md            This file
DESIGN.md / .docx    Full technical design document
```

---

## 🔑 API Keys

| Provider | Where to get | Key format |
|---|---|---|
| Anthropic | console.anthropic.com | `sk-ant-…` |
| OpenAI | platform.openai.com/api-keys | `sk-…` |
| Google Gemini | aistudio.google.com/app/apikey | `AIza…` |
| Groq | console.groq.com/keys | `gsk_…` |

Keys are stored only in your browser's `localStorage` under `nt_v6_key_{provider}`. They never leave your device except in direct API calls to the respective provider.

---

## ⚙️ Configuration

All configuration is in-file JavaScript constants:

```javascript
// Main tool provider/model selector
const PROVIDERS = { anthropic: {...}, openai: {...}, gemini: {...}, groq: {...} }

// Debate arena providers
const DB_PROVIDERS = { anthropic: {...}, openai: {...}, gemini: {...}, groq: {...} }

// Domain expert definitions  
const DB_DOMAINS = [ ...10 domain objects with keywords, role, desc... ]
```

---

## 🧩 Key Design Decisions

**Why a single HTML file?**
Zero deployment friction. Works offline after first load. Share by attaching to an email. No CORS, no CDN, no build pipeline.

**Why vanilla JS with no framework?**
The app is UI-light but logic-heavy. React/Vue would add ~100KB for no benefit. Vanilla JS is faster to load, easier to inspect, and has no dependency rot.

**Why streaming instead of waiting for full response?**
A system design answer takes 15-25 seconds at full quality. Streaming with a skeleton UI makes the wait feel like ~3-4 seconds by showing meaningful content immediately.

**Why multi-attempt JSON parsing?**
LLMs occasionally emit leading text before `{`, trailing commas, or truncated JSON under rate pressure. The 4-step parse strategy recovers gracefully rather than showing an error.

**Why the debate arena uses non-streaming for Phase 1/2/3?**
Streaming works well for one long answer. For 4 parallel answers + critiques + a judge, streaming would create a chaotic UI. Collecting full responses before rendering gives a cleaner phase-by-phase progression.

---

## 🔒 Privacy & Security

- **API keys** stored in `localStorage` only — never sent to any server except the respective AI provider
- **Questions and answers** sent directly from your browser to the AI provider — nothing passes through any intermediate server
- **No analytics, no tracking, no ads**
- **No account required**

---

## 📄 License

MIT — use freely, modify freely, no attribution required.
