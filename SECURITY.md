<div align="center">

# 🔒 Godlike-Chat — Security, Architecture & Data Safety

### Complete Technical Documentation

[![Status](https://img.shields.io/badge/Status-Production--Ready-brightgreen?style=for-the-badge)](.)
[![Framework](https://img.shields.io/badge/Framework-Next.js%2015-black?style=for-the-badge&logo=next.js)](.)
[![AI](https://img.shields.io/badge/AI-NVIDIA%20NIM-76B900?style=for-the-badge&logo=nvidia)](.)
[![License](https://img.shields.io/badge/License-Private-red?style=for-the-badge)](.)

---

*Last Updated: April 7, 2026*

</div>

---

## 📑 Table of Contents

- [🏗️ System Architecture](#️-system-architecture)
- [🌳 Control Flow Tree](#-control-flow-tree)
- [🔐 Security Model](#-security-model)
- [📡 API Route Deep Dive](#-api-route-deep-dive)
- [🛡️ Data Privacy & Safety](#️-data-privacy--safety)
- [⚠️ Known Risks & Mitigations](#️-known-risks--mitigations)
- [✅ Final Verdict — Is It Safe?](#-final-verdict--is-it-safe)

---

## 🏗️ System Architecture

Godlike-chat is a **local-first, self-hosted** AI chatbot that runs entirely on your own Windows PC. Here is how every piece connects:

```
┌─────────────────────────────────────────────────────────────────────┐
│                        YOUR WINDOWS PC                              │
│                                                                     │
│  ┌──────────────────────────────────────────────────────────────┐   │
│  │                  🌐 Browser (localhost:3000)                  │   │
│  │  ┌────────────────────────────────────────────────────────┐  │   │
│  │  │              React Frontend (page.js)                  │  │   │
│  │  │                                                        │  │   │
│  │  │  • Chat UI, Settings, Themes, Voice, WakeWord          │  │   │
│  │  │  • localStorage (chats, keys, memories, settings)      │  │   │
│  │  │  • Speech Recognition & Synthesis (Web Speech API)     │  │   │
│  │  └─────────────┬──────────────────────────────────────────┘  │   │
│  │                │ HTTP (localhost only)                        │   │
│  │  ┌─────────────▼──────────────────────────────────────────┐  │   │
│  │  │           Next.js API Routes (Backend)                 │  │   │
│  │  │                                                        │  │   │
│  │  │  /api/chat ────────── NVIDIA NIM Cloud ───── (HTTPS)   │  │   │
│  │  │  /api/title ───────── NVIDIA NIM Cloud ───── (HTTPS)   │  │   │
│  │  │  /api/memory ──────── NVIDIA NIM Cloud ───── (HTTPS)   │  │   │
│  │  │  /api/system ──────── Local OS Commands ──── (LOCAL)   │  │   │
│  │  │  /api/screenshot ──── Local PowerShell ───── (LOCAL)   │  │   │
│  │  │  /api/scrape ──────── External Websites ──── (HTTPS)   │  │   │
│  │  │  /api/websearch ───── DuckDuckGo HTML ────── (HTTPS)   │  │   │
│  │  │  /api/ip ──────────── Local Network Info ─── (LOCAL)   │  │   │
│  │  └────────────────────────────────────────────────────────┘  │   │
│  └──────────────────────────────────────────────────────────────┘   │
│                                                                     │
│  ┌──────────────────────┐    ┌───────────────────────────────┐     │
│  │  📁 File System       │    │  🖥️ Windows OS               │     │
│  │  (read/write files)   │    │  (open/close apps, volume,   │     │
│  │                       │    │   lock screen, keystrokes)    │     │
│  └──────────────────────┘    └───────────────────────────────┘     │
└─────────────────────────────────────────────────────────────────────┘
                          │
                          │ HTTPS (encrypted)
                          ▼
              ┌──────────────────────┐
              │  ☁️  NVIDIA NIM API   │
              │  (Cloud LLM Server)  │
              │                      │
              │  • Receives prompts  │
              │  • Returns responses │
              │  • No storage (*)    │
              └──────────────────────┘
```

> **Key Insight:** Your app is a **hybrid** — the UI and system control run 100% locally, but the AI brain (LLM inference) is powered by NVIDIA's cloud API.

---

## 🌳 Control Flow Tree

This tree shows **exactly what happens** from the moment you type a message to the moment the AI responds and executes actions.

```
👤 User Types Message & Presses Enter
│
├── 1️⃣  Frontend: handleSend()
│   ├── Strip mic preview text (🎤...)
│   ├── Check for URLs in message
│   │   └── YES → Call /api/scrape for each URL
│   │       └── Append scraped content to message
│   ├── Add message to state: messages[]
│   └── Call sendMessages(msgs)
│
├── 2️⃣  Frontend: sendMessages(msgs, depth=0)
│   ├── Check depth < MAX_DEPTH (5) → Prevent infinite loops
│   ├── Build System Prompt:
│   │   ├── Memory Context (user facts)
│   │   ├── Web Directive (HTML code blocks)
│   │   ├── Think Directive (if Deep Think ON)
│   │   ├── PC Directive (if System Access ON)
│   │   ├── Voice Directive (if voice mode active)
│   │   └── Custom System Prompt
│   └── POST /api/chat (streaming)
│
├── 3️⃣  Backend: /api/chat
│   ├── Validate API key exists
│   ├── Clean API key (remove newlines)
│   ├── Build final messages array
│   │   ├── System prompt (uncensored or custom)
│   │   ├── Attach file content if present
│   │   └── User conversation history
│   ├── Call NVIDIA NIM API (HTTPS, streaming)
│   └── Stream response chunks back to frontend
│
├── 4️⃣  Frontend: Process Stream
│   ├── Append chunks to last assistant message
│   ├── If alwaysTalk → Queue speech chunks
│   └── On stream complete:
│       │
│       ├── 🔍 Check for JSON tool blocks (if System Access ON)
│       │   │
│       │   ├── action: "web_search"
│       │   │   └── POST /api/websearch → DuckDuckGo
│       │   │
│       │   ├── action: "scrape_url"
│       │   │   └── POST /api/scrape → Fetch & parse website
│       │   │
│       │   ├── action: "save_memory"
│       │   │   └── Save fact to localStorage
│       │   │
│       │   ├── action: "screenshot"
│       │   │   └── POST /api/screenshot → PowerShell (window titles)
│       │   │
│       │   ├── action: "open_app" / "close_app"
│       │   │   └── POST /api/system → start/taskkill (AUTH REQUIRED)
│       │   │
│       │   ├── action: "run_command"
│       │   │   └── POST /api/system → exec() (AUTH REQUIRED)
│       │   │
│       │   ├── action: "type_text"
│       │   │   └── POST /api/system → PowerShell SendKeys (AUTH REQUIRED)
│       │   │
│       │   ├── action: "read_file" / "write_file" / "list_dir" ...
│       │   │   └── POST /api/system → fs operations (AUTH + PATH CHECK)
│       │   │
│       │   └── action: "open_url"
│       │       └── POST /api/system → start URL (PROTOCOL CHECK)
│       │
│       ├── 📨 Collect all tool outputs
│       ├── 🔄 Feed outputs back as new user message
│       └── 🔁 Recursive: sendMessages(newMsgs, depth+1)
│           └── (Max 5 rounds, then stops)
│
├── 5️⃣  Post-Response
│   ├── Auto-title chat (if first message)
│   ├── Extract memory (every 4th message pair)
│   ├── Re-arm wake word listener
│   └── Save chat to localStorage
│
└── 💾 All Data Stored in Browser localStorage
    ├── nvidia_api_key
    ├── nvidia_chats (all conversations)
    ├── nvidia_user_memory (extracted facts)
    ├── nvidia_theme, nvidia_lang, nvidia_fontsize
    └── nvidia_pin_hash (lock screen PIN)
```

---

## 🔐 Security Model

### Layer 1: API Key Protection

| Aspect | Implementation | Safety Rating |
|---|---|---|
| **Storage** | Browser `localStorage` only | ⚠️ Medium |
| **Transmission** | Sent to Next.js backend via `localhost` (never leaves your PC) | ✅ Safe |
| **To NVIDIA** | Sent over HTTPS (TLS encrypted) | ✅ Safe |
| **Sanitization** | Newlines and carriage returns stripped | ✅ Safe |
| **Exposure Risk** | Visible in browser DevTools if someone accesses your PC | ⚠️ Medium |

> **💡 Note:** Your API key **never touches any third-party server** other than NVIDIA's official API endpoint (`integrate.api.nvidia.com`). It goes:
> `Browser → localhost:3000 → NVIDIA API (HTTPS)`

---

### Layer 2: System API Authentication

The `/api/system` route (which controls your PC) is protected by a **Bearer Token** system:

```
┌──────────────┐     Authorization: Bearer godlike-local-only     ┌──────────────┐
│   Frontend    │ ──────────────────────────────────────────────► │  /api/system  │
│  (Browser)    │                                                 │   (Backend)   │
└──────────────┘                                                  └──────┬───────┘
                                                                         │
                                                               Token Match? 
                                                                    │
                                                          ┌─────────┴─────────┐
                                                          │                   │
                                                       ✅ YES              ❌ NO
                                                          │                   │
                                                    Execute Action     403 Forbidden
```

**Security Controls:**
- ✅ **Action Whitelist** — Only 19 predefined actions are allowed. Any unknown action is rejected.
- ✅ **Input Sanitization** — App names are stripped of special characters (`& | ; > < \n \r $ () {}`)
- ✅ **Blocked Commands** — Dangerous commands like `format`, `del /s`, `rm -rf`, `shutdown`, `reg delete` are hardcoded blocked
- ✅ **Blocked Paths** — File operations cannot touch `System32`, `.ssh`, `.env`, `.git/config`
- ✅ **File Size Limits** — Max 1MB for read/write operations
- ✅ **URL Protocol Check** — Only `http://` and `https://` URLs can be opened
- ✅ **Command Timeout** — 30-second timeout on all executed commands
- ✅ **Agent Loop Limit** — Maximum 5 autonomous rounds to prevent infinite loops

---

### Layer 3: Web Scraping Safety (SSRF Prevention)

The `/api/scrape` route has **Server-Side Request Forgery (SSRF) protection**:

```
 Incoming URL ──► Protocol Check ──► IP Range Check ──► Port Check ──► ✅ Allowed
                       │                    │                │
                       ▼                    ▼                ▼
                  Only http/https     Block private IPs   Block internal
                  (no file://, etc)   • 10.x.x.x         ports (3000,
                                      • 172.16-31.x.x     8080, 5432,
                                      • 192.168.x.x       etc.)
                                      • 169.254.x.x
                                      • localhost
                                      • 127.0.0.1
```

---

### Layer 4: App-Level Security

| Feature | How It Works |
|---|---|
| **PIN Lock** | SHA-256 hashed PIN stored in localStorage. Blocks UI access on app load. |
| **Auto-Scroll Protection** | Prevents automatic scrolling hijack when user is reading old messages |
| **Abort Controller** | Any AI generation can be immediately cancelled by the user |
| **Content Truncation** | Scraped web content capped at 15,000 chars, file content capped at 1MB |

---

## 📡 API Route Deep Dive

### Route Architecture Tree

```
/api/
├── chat/           🧠 Core AI conversation (NVIDIA NIM)
│   ├── Input:  messages[], apiKey, model, systemPrompt
│   ├── Output: Streaming text response
│   └── External: integrate.api.nvidia.com (HTTPS)
│
├── system/         🖥️ PC Control & File Operations (AUTH REQUIRED)
│   ├── Input:  action, appName, text, path, command, url, query
│   ├── Actions: 19 whitelisted operations
│   └── External: NONE (local OS only)
│
├── screenshot/     📸 Window Context Reader
│   ├── Input:  (none)
│   ├── Output: List of open window titles + active window
│   └── External: NONE (local PowerShell)
│
├── scrape/         🕸️ Web Page Text Extractor
│   ├── Input:  url
│   ├── Output: Cleaned text content (max 15KB)
│   └── External: Target website (HTTPS, SSRF-protected)
│
├── websearch/      🔍 Privacy-First Web Search
│   ├── Input:  query
│   ├── Output: Top 6 search results (title, snippet, URL)
│   └── External: html.duckduckgo.com (no tracking)
│
├── memory/         🧠 Automatic Fact Extractor
│   ├── Input:  messages[], apiKey
│   ├── Output: Array of extracted user facts
│   └── External: integrate.api.nvidia.com (HTTPS)
│
├── title/          📝 Auto Chat Title Generator
│   ├── Input:  messages[], apiKey
│   ├── Output: Short title (max 5 words)
│   └── External: integrate.api.nvidia.com (HTTPS)
│
└── ip/             📱 LAN IP Discovery (for QR code)
    ├── Input:  (none)
    ├── Output: Array of local IPv4 addresses
    └── External: NONE (local OS)
```

---

## 🛡️ Data Privacy & Safety

### Where Does Your Data Go?

```
┌─────────────────────────────────────────────────────────────────┐
│                    DATA FLOW MAP                                 │
├─────────────────────────────────────────────────────────────────┤
│                                                                 │
│  📝 Your Messages                                               │
│  ├── ✅ Stored in browser localStorage (YOUR PC only)           │
│  ├── ⚠️ Sent to NVIDIA NIM API for AI processing               │
│  └── ❌ NOT sent to any other third party                       │
│                                                                 │
│  🔑 Your API Key                                                │
│  ├── ✅ Stored in browser localStorage (YOUR PC only)           │
│  ├── ✅ Sent to NVIDIA over HTTPS (encrypted in transit)        │
│  └── ❌ NOT logged, shared, or sent elsewhere                   │
│                                                                 │
│  🧠 Your Memories (extracted facts)                             │
│  ├── ✅ Stored in browser localStorage (YOUR PC only)           │
│  └── ❌ NOT sent externally (used only in-prompt as context)    │
│                                                                 │
│  🔍 Your Search Queries                                         │
│  ├── ✅ Sent to DuckDuckGo (privacy-focused, no tracking)      │
│  └── ❌ NOT sent to Google, Bing, or any tracker                │
│                                                                 │
│  🖥️ System Commands                                             │
│  ├── ✅ Executed 100% locally via PowerShell/CMD                │
│  └── ❌ NOT transmitted over the network                        │
│                                                                 │
│  📁 File Operations                                             │
│  ├── ✅ Executed 100% locally via Node.js fs module             │
│  └── ❌ File contents NEVER leave your machine                  │
│                                                                 │
└─────────────────────────────────────────────────────────────────┘
```

### NVIDIA NIM API — What Do They See?

| Data Point | Sent to NVIDIA? | Details |
|---|---|---|
| Your chat messages | ✅ Yes | Required for AI to generate responses |
| Your API key | ✅ Yes | Required for authentication |
| Your system prompt | ✅ Yes | Included in the request |
| Your memory facts | ✅ Yes | Injected into system prompt context |
| Your file contents (attached) | ✅ Yes | Appended to last user message |
| Your PC file system data | ❌ No | Stays local (never in prompts unless AI writes code that reads it) |
| Your passwords/PIN | ❌ No | Stored as SHA-256 hash, never transmitted |
| Your theme/settings | ❌ No | Purely local localStorage |

> **⚠️ IMPORTANT:** According to NVIDIA's [NIM API Terms](https://build.nvidia.com), data sent via the free-tier API **may be used to improve models**. If this concerns you, consider:
> 1. Using a paid NVIDIA API tier (they offer data-privacy guarantees)
> 2. Avoiding sending sensitive personal information in chat messages
> 3. Self-hosting an open-source LLM locally (e.g., Ollama + Llama 3)

---

## ⚠️ Known Risks & Mitigations

### Risk Assessment Matrix

| Risk | Severity | Likelihood | Mitigation Status |
|---|:---:|:---:|:---:|
| API key visible in DevTools | 🟡 Medium | Low | ⚠️ Use PIN lock |
| NVIDIA reads your prompts (free tier) | 🟡 Medium | Possible | ⚠️ Don't share secrets in chat |
| `run_command` executes arbitrary code | 🔴 High | Low | ✅ Blocked patterns + auth token |
| System API exposed on LAN | 🟡 Medium | Low | ✅ Bearer token required |
| File operations on sensitive paths | 🔴 High | Low | ✅ Blocked path patterns |
| Infinite agent loop | 🟡 Medium | Low | ✅ Max depth = 5 rounds |
| XSS via AI-generated HTML | 🟡 Medium | Low | ✅ ReactMarkdown sanitizes output |
| SSRF via scrape endpoint | 🔴 High | Low | ✅ Private IP + port blocking |
| Wake word false activation | 🟢 Low | Medium | ⚠️ Multiple fuzzy matches used |

### What The System **Cannot** Do (Safety Guardrails)

```
❌ Cannot access System32 or Windows system files
❌ Cannot read .ssh keys, .env files, or .git configs
❌ Cannot run: format, del /s, rmdir /s, rm -rf, shutdown
❌ Cannot run: reg delete, net user, net localgroup
❌ Cannot open non-HTTP URLs (no file://, ftp://, etc.)
❌ Cannot scrape localhost, 127.0.0.1, or private IPs
❌ Cannot read/write files larger than 1MB
❌ Cannot loop more than 5 times autonomously
❌ Cannot execute commands longer than 30 seconds
```

---

## ✅ Final Verdict — Is It Safe?

<table>
<tr>
<td width="50%">

### ✅ YES — Safe For Personal Use

**When used as intended (locally, by you, on your own PC):**
- All data stays on your machine (localStorage)
- System API is auth-protected
- Dangerous operations are blocked
- Web scraping has SSRF protection
- Search uses privacy-respecting DuckDuckGo
- No third-party analytics or trackers
- No cookies sent to external services
- PIN lock available for UI access

</td>
<td width="50%">

### ⚠️ CAUTION — Risks To Be Aware Of

**Things that require your awareness:**
- NVIDIA free-tier may process your prompts
- API key stored in plain text in localStorage
- `run_command` action is powerful (use carefully)
- `type_text` can send keystrokes to any app
- If someone accesses your PC, they can read your chats
- The Bearer token is hardcoded (not per-session)
- LAN users could potentially access the UI (use PIN)

</td>
</tr>
</table>

### 🏆 Overall Safety Score

```
 ██████████████████████████████████████████░░░░░░░  82 / 100
 ├── Authentication     ████████░░  8/10
 ├── Data Privacy       ███████░░░  7/10
 ├── Input Validation   █████████░  9/10
 ├── Path Protection    █████████░  9/10
 ├── Network Safety     ████████░░  8/10
 ├── Error Handling     ████████░░  8/10
 └── Code Execution     ███████░░░  7/10  (inherently risky feature)
```

---

### 🔧 Recommendations To Maximize Safety

1. **Set a SYSTEM_SECRET** — Add `SYSTEM_SECRET=your-random-string-here` to your `.env.local` file to replace the default token
2. **Enable PIN Lock** — Go to Settings → Advanced → Set a PIN (at least 6 characters)
3. **Don't paste passwords into chat** — The AI sends your messages to NVIDIA
4. **Keep System Access OFF** unless needed — Only enable `💻 System Access` when you specifically need PC control
5. **Use a firewall** — Block port 3000 from LAN if you don't want mobile QR access

---

<div align="center">

### 🛡️ Built with security in mind by [@Nothing-dot-exe](https://github.com/Nothing-dot-exe)

*Godlike-chat v2.0 — Your Local AI Assistant*

</div>
