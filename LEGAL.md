<div align="center">

# ⚖️ Godlike-Chat — Legal Document

### Terms of Use · Privacy Policy · License · Disclaimer

[![Legal](https://img.shields.io/badge/Document-Legal-gold?style=for-the-badge)](.)
[![Version](https://img.shields.io/badge/Version-2.0-blue?style=for-the-badge)](.)
[![Effective](https://img.shields.io/badge/Effective-April_2026-green?style=for-the-badge)](.)

---

*Effective Date: April 7, 2026 · Last Updated: April 7, 2026*

</div>

---

## 📑 Table of Contents

1. [📜 Terms of Use](#1--terms-of-use)
2. [🔒 Privacy Policy](#2--privacy-policy)
3. [📄 Software License](#3--software-license)
4. [⚠️ Disclaimer of Warranties](#4-️-disclaimer-of-warranties)
5. [🚫 Limitation of Liability](#5--limitation-of-liability)
6. [😈 Uncensored Mode — Special Terms](#6--uncensored-mode--special-terms)
7. [🖥️ System Access — Special Terms](#7-️-system-access--special-terms)
8. [🌐 Third-Party Services](#8--third-party-services)
9. [👤 User Responsibilities](#9--user-responsibilities)
10. [📝 Changes to This Document](#10--changes-to-this-document)
11. [📧 Contact Information](#11--contact-information)

---

## 1. 📜 Terms of Use

### 1.1 Acceptance of Terms

By downloading, installing, accessing, or using Godlike-chat ("the Software", "the Application", "the App"), you ("the User", "you") agree to be bound by these Terms of Use, Privacy Policy, and all applicable laws and regulations. If you do not agree with any of these terms, you are prohibited from using the Software.

### 1.2 Description of Service

Godlike-chat is a **self-hosted, local-first AI chatbot application** that provides:

| Feature | Description |
|---|---|
| AI Chat | Conversational AI powered by NVIDIA NIM API |
| Multi-Model Support | Access to Llama 3.1 (8B, 70B, 405B) and Mixtral 8x22B |
| Uncensored Mode | Optional unfiltered AI response mode |
| System Access | Optional local PC control capabilities |
| Voice Interface | Speech-to-text and text-to-speech |
| Web Search | Privacy-focused search via DuckDuckGo |
| Web Scraping | URL content extraction |
| File Operations | Local file read/write capabilities |
| Memory System | Automatic user preference learning |

### 1.3 Eligibility

- You must be at least **18 years of age** to use Uncensored Mode.
- You must be at least **13 years of age** to use the Application in Censored Mode.
- You must have **legal authorization** to use the NVIDIA NIM API in your jurisdiction.
- You must have **administrative access** to the computer on which you install the Software.

### 1.4 API Key Requirement

The Application requires a valid NVIDIA NIM API key to function. By providing your API key:
- You confirm that the key belongs to you or that you have authorization to use it.
- You acknowledge that you are solely responsible for any charges, rate limits, or terms of service violations associated with your API key usage.
- You understand that the Application stores your API key locally in your browser's `localStorage`.

---

## 2. 🔒 Privacy Policy

### 2.1 Data We Collect

Godlike-chat is designed with a **privacy-first architecture**. The Application itself does not have its own servers, databases, or analytics systems.

```
┌─────────────────────────────────────────────────────────┐
│              DATA COLLECTION SUMMARY                     │
├──────────────────────┬──────────────────────────────────┤
│  Data Type           │  Where It's Stored               │
├──────────────────────┼──────────────────────────────────┤
│  Chat Messages       │  Browser localStorage (YOUR PC)  │
│  API Key             │  Browser localStorage (YOUR PC)  │
│  User Memories       │  Browser localStorage (YOUR PC)  │
│  Settings/Themes     │  Browser localStorage (YOUR PC)  │
│  PIN Hash            │  Browser localStorage (YOUR PC)  │
│  Chat History        │  Browser localStorage (YOUR PC)  │
├──────────────────────┼──────────────────────────────────┤
│  ❌ We do NOT have:  │  No servers, no databases,       │
│                      │  no analytics, no cookies,       │
│                      │  no tracking pixels,             │
│                      │  no user accounts                │
└──────────────────────┴──────────────────────────────────┘
```

### 2.2 Data Shared with Third Parties

| Third Party | What's Shared | Why | Their Privacy Policy |
|---|---|---|---|
| **NVIDIA NIM API** | Your chat messages, system prompt, API key | Required for AI inference | [NVIDIA Privacy](https://www.nvidia.com/en-us/about-nvidia/privacy-policy/) |
| **DuckDuckGo** | Search queries (via `/api/websearch`) | Web search functionality | [DuckDuckGo Privacy](https://duckduckgo.com/privacy) |
| **Target Websites** | Your IP address (via `/api/scrape`) | URL content extraction | Varies by website |

### 2.3 NVIDIA NIM API Data Handling

> **⚠️ IMPORTANT NOTICE:**
>
> When using the **free tier** of the NVIDIA NIM API, your prompts and conversations MAY be used by NVIDIA for model improvement and research purposes, in accordance with NVIDIA's own terms of service.
>
> **If you are concerned about data privacy:**
> - Consider using a **paid NVIDIA API tier** which offers data privacy guarantees
> - Avoid sharing sensitive personal information (passwords, financial data, medical records) in chat messages
> - Consider **self-hosting** an open-source LLM locally using tools like Ollama

### 2.4 Local Data Processing

The following operations are performed **entirely on your local machine** with no data leaving your PC:

- ✅ File system operations (read, write, delete, rename)
- ✅ System commands (open/close apps, volume control, lock screen)
- ✅ Keystroke simulation (type_text action)
- ✅ Screenshot/window detection
- ✅ PIN hashing and verification
- ✅ Speech recognition and synthesis
- ✅ Theme, language, and UI preference management

### 2.5 Data Retention

- **By You:** All data is stored in your browser's `localStorage` indefinitely until you manually clear it or use the "Factory Reset" feature.
- **By NVIDIA:** Subject to NVIDIA's data retention policies.
- **By DuckDuckGo:** DuckDuckGo does not store search histories per their privacy policy.
- **By Us:** We retain **zero** user data. We have no servers. We cannot access your data.

### 2.6 Your Rights

Since all data is stored locally on your device:
- **Right to Access:** Open browser DevTools → Application → Local Storage to view all stored data.
- **Right to Delete:** Use Settings → "Factory Reset App" to permanently erase all data.
- **Right to Export:** Use Settings → "Export JSON" or "Export TXT" to download your chat history.
- **Right to Portability:** Your data is stored in standard JSON format, fully portable.

---

## 3. 📄 Software License

### 3.1 License Grant

```
Copyright (c) 2026 Nothing-dot-exe
All Rights Reserved.
```

This software is provided as **proprietary source-available software**. You are granted a limited, non-exclusive, non-transferable, revocable license to:

- ✅ **Use** the Software for personal, non-commercial purposes
- ✅ **Modify** the Software for your own personal use
- ✅ **Study** the source code for educational purposes
- ✅ **Run** the Software on your own hardware

### 3.2 Restrictions

You may NOT:

- ❌ **Sell, sublicense, or commercially distribute** the Software or any derivative works
- ❌ **Remove or alter** any copyright notices, branding, or attribution
- ❌ **Claim authorship** of the Software or represent it as your own creation
- ❌ **Use the Software** to provide services to third parties (SaaS) without written permission
- ❌ **Deploy the Software** on public-facing servers accessible to unauthorized users without appropriate security measures

### 3.3 Attribution

If you share, fork, or reference this project, you must provide clear attribution to:

```
Godlike-chat by @Nothing-dot-exe
https://github.com/Nothing-dot-exe
```

### 3.4 Open-Source Dependencies

This Software incorporates the following open-source libraries, each subject to their own licenses:

| Library | License | Purpose |
|---|---|---|
| Next.js | MIT | Web framework |
| React | MIT | UI library |
| OpenAI SDK | Apache 2.0 | NVIDIA NIM API client |
| Cheerio | MIT | HTML parsing (scraping) |
| react-markdown | MIT | Markdown rendering |
| remark-gfm | MIT | GitHub Flavored Markdown |
| qrcode.react | ISC | QR code generation |

---

## 4. ⚠️ Disclaimer of Warranties

```
THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND,
EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES
OF MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE, AND
NONINFRINGEMENT.

IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE LIABLE
FOR ANY CLAIM, DAMAGES, OR OTHER LIABILITY, WHETHER IN AN
ACTION OF CONTRACT, TORT, OR OTHERWISE, ARISING FROM, OUT OF,
OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER
DEALINGS IN THE SOFTWARE.
```

### Specifically:

- **No Guarantee of AI Accuracy:** The AI may generate incorrect, misleading, or fabricated information ("hallucinations"). Do not rely on AI-generated content for medical, legal, financial, or safety-critical decisions.
- **No Guarantee of Availability:** NVIDIA's API may experience downtime, rate limiting, or service changes beyond our control.
- **No Guarantee of Security:** While we implement reasonable security measures (Bearer token auth, path blocking, command blocking, SSRF prevention), no software is immune to vulnerabilities. The System Access feature inherently carries risk.
- **No Professional Advice:** AI responses do not constitute professional advice of any kind (medical, legal, financial, psychological, or otherwise).

---

## 5. 🚫 Limitation of Liability

### 5.1 General Limitation

To the maximum extent permitted by applicable law, in no event shall the developer(s) of Godlike-chat be liable for:

- Any **direct, indirect, incidental, special, consequential, or punitive damages**
- Any **loss of profits, data, business opportunities, or goodwill**
- Any **damage to your computer, operating system, files, or hardware**
- Any **unauthorized access to your data** resulting from use of the Software
- Any **actions taken by the AI** including system commands, file operations, or network requests
- Any **content generated by the AI** that is inaccurate, offensive, harmful, or illegal

### 5.2 System Access Liability

> **🚨 CRITICAL:**
>
> The System Access feature (`💻 System Access` toggle) grants the AI the ability to execute commands on your operating system, read/write files, open/close applications, and send keystrokes. By enabling this feature:
>
> - **YOU assume ALL risk** for any actions the AI performs on your computer.
> - The developer is **NOT liable** for any data loss, system damage, or unintended actions.
> - You acknowledge that even with safety guards (blocked commands, path restrictions), the AI could potentially execute harmful operations through indirect methods.

### 5.3 Maximum Liability

In jurisdictions that do not allow the exclusion of certain warranties or limitation of liability, our liability shall be limited to the **maximum extent permitted by law**, which in all cases shall not exceed **$0 USD** (the price you paid for the Software).

---

## 6. 😈 Uncensored Mode — Special Terms

### 6.1 Nature of Uncensored Mode

Uncensored Mode modifies the AI's system prompt to reduce content filtering and safety guardrails. When enabled:

- The AI **will not refuse** most questions
- The AI **will not add** safety disclaimers or moral commentary
- The AI **may generate** content that is explicit, controversial, offensive, or disturbing
- The AI's temperature is increased to **0.9** for more creative/unrestricted outputs

### 6.2 User Responsibility

By enabling Uncensored Mode, you acknowledge and agree that:

1. **You are at least 18 years of age.**
2. **You are solely responsible** for any content generated while Uncensored Mode is active.
3. **You will not use** Uncensored Mode to generate content that violates local, state, national, or international laws.
4. **You will not use** Uncensored Mode to generate content intended to harm, harass, threaten, or defraud any individual or group.
5. **You will not use** Uncensored Mode to generate malware, exploit code, or tools designed for illegal unauthorized access.
6. **The developer is NOT responsible** for any AI-generated content produced in Uncensored Mode.

### 6.3 Prohibited Uses

The following uses of Uncensored Mode are strictly prohibited:

| Category | Examples |
|---|---|
| **Illegal Content** | Content that violates applicable laws in your jurisdiction |
| **CSAM** | Any content sexualizing minors in any form |
| **Real Violence** | Planning or facilitating real-world violence against specific individuals |
| **Fraud** | Generating content designed to deceive or defraud others |
| **Impersonation** | Creating AI-generated content falsely attributed to real people |
| **Malware** | Generating functional malware, ransomware, or exploit payloads intended for malicious use |

### 6.4 Residual Filtering

Even with Uncensored Mode enabled, NVIDIA's server-side API may still reject certain requests at the infrastructure level. This is beyond our control and represents NVIDIA's independent content policy enforcement.

---

## 7. 🖥️ System Access — Special Terms

### 7.1 Capabilities

When System Access is enabled, the AI can:

```
┌────────────────────────────────────────────────────────────┐
│  SYSTEM ACCESS CAPABILITIES                                 │
├────────────────────────────────────────────────────────────┤
│                                                            │
│  📂 FILE SYSTEM          │  🖥️ SYSTEM CONTROL              │
│  • Read files            │  • Open applications            │
│  • Write/create files    │  • Close applications           │
│  • Delete files          │  • Volume up/down/mute          │
│  • Rename files          │  • Lock screen                  │
│  • Create directories    │  • List open windows            │
│  • Delete directories    │  • Take screenshots             │
│  • List directories      │  • Type text (keystrokes)       │
│                          │  • Run shell commands           │
│  🌐 NETWORK              │                                 │
│  • Open URLs             │  🧠 MEMORY                      │
│  • Web search            │  • Save facts about you         │
│  • Scrape web pages      │                                 │
│                          │                                 │
└────────────────────────────────────────────────────────────┘
```

### 7.2 Safety Measures Implemented

| Safety Layer | Implementation |
|---|---|
| Authentication | Bearer token required for all system calls |
| Action Whitelist | Only 19 predefined actions accepted |
| Command Blocking | `format`, `del /s`, `rmdir /s`, `rm -rf`, `shutdown`, `reg delete`, `net user` blocked |
| Path Blocking | `System32`, `.ssh`, `.env`, `.git/config` paths blocked |
| File Size Limit | Max 1MB for read/write operations |
| URL Protocol Check | Only `http://` and `https://` allowed |
| SSRF Prevention | Localhost, private IPs, and internal ports blocked |
| Timeout | 30-second timeout on all commands |
| Loop Limit | Max 5 autonomous execution rounds |
| Input Sanitization | Special characters stripped from app names |

### 7.3 Assumption of Risk

> **By enabling System Access, you explicitly acknowledge that:**
>
> 1. The AI is controlling your actual operating system, not a sandbox.
> 2. Actions are **irreversible** — deleted files cannot be recovered through the Application.
> 3. The AI may **misinterpret** your instructions and execute unintended actions.
> 4. Safety measures reduce but **do not eliminate** risk.
> 5. You should **back up important data** before granting the AI system access.
> 6. **Advanced System Access** mode removes additional protections and should only be used if you fully understand the risks.

---

## 8. 🌐 Third-Party Services

### 8.1 NVIDIA NIM API

- **Provider:** NVIDIA Corporation
- **Service:** Cloud-based LLM inference
- **Terms:** Subject to [NVIDIA's Terms of Use](https://www.nvidia.com/en-us/about-nvidia/legal-info/)
- **Data Handling:** Subject to [NVIDIA's Privacy Policy](https://www.nvidia.com/en-us/about-nvidia/privacy-policy/)
- **Relationship:** Godlike-chat is an independent project and is NOT affiliated with, endorsed by, or sponsored by NVIDIA Corporation.

### 8.2 DuckDuckGo

- **Provider:** DuckDuckGo, Inc.
- **Service:** Privacy-focused web search
- **Terms:** Subject to [DuckDuckGo's Terms of Service](https://duckduckgo.com/terms)
- **Relationship:** We use DuckDuckGo's public HTML search interface. We are not affiliated with DuckDuckGo.

### 8.3 Web Speech API

- **Provider:** Your browser vendor (Google Chrome, Microsoft Edge, etc.)
- **Service:** Speech recognition and speech synthesis
- **Note:** Speech recognition data may be processed by your browser vendor's servers (e.g., Google's servers for Chrome). This is controlled by your browser, not by Godlike-chat.

---

## 9. 👤 User Responsibilities

By using Godlike-chat, you agree to:

### 9.1 General Responsibilities

- ✅ Use the Software in compliance with all applicable laws and regulations
- ✅ Keep your NVIDIA API key confidential and secure
- ✅ Use the PIN lock feature if the device is shared with others
- ✅ Review AI-generated content before acting on it
- ✅ Maintain backups of important files before using System Access features
- ✅ Report any security vulnerabilities responsibly

### 9.2 Prohibited Activities

- ❌ Using the Software to violate any law, regulation, or third-party rights
- ❌ Using the Software to generate unlawful content
- ❌ Attempting to circumvent NVIDIA's API rate limits or terms of service
- ❌ Using the Software to attack, probe, or exploit other computer systems
- ❌ Redistributing the Software commercially without authorization
- ❌ Using the Software to build competitive commercial products

### 9.3 Compliance with Local Laws

You are solely responsible for ensuring that your use of Godlike-chat, including the Uncensored Mode and System Access features, complies with the laws of your jurisdiction. Laws regarding AI-generated content, computer access, and data privacy vary significantly across jurisdictions.

---

## 10. 📝 Changes to This Document

- We reserve the right to modify these terms at any time.
- Changes will be reflected in the "Last Updated" date at the top of this document.
- Continued use of the Software after changes constitutes acceptance of the revised terms.
- Material changes will be noted in the project's `CHANGELOG.md` or `README.md`.

---

## 11. 📧 Contact Information

For questions, concerns, or security reports regarding this document or the Software:

| Channel | Details |
|---|---|
| **Developer** | @Nothing-dot-exe |
| **GitHub** | [github.com/Nothing-dot-exe](https://github.com/Nothing-dot-exe) |
| **Issues** | File an issue on the GitHub repository |

---

## 📋 Summary Table

| Topic | Status |
|---|---|
| Do we have servers? | ❌ No — fully local |
| Do we collect user data? | ❌ No — all in localStorage |
| Do we track you? | ❌ No — zero analytics |
| Is your API key safe? | ⚠️ Stored locally in plaintext (use PIN lock) |
| Does NVIDIA see your chats? | ✅ Yes — required for AI to work |
| Can the AI damage your PC? | ⚠️ Possible with System Access ON |
| Is Uncensored Mode legal? | ✅ The tool itself is legal; the content you generate is your responsibility |
| Can you delete all data? | ✅ Yes — Factory Reset in Settings |
| Is this open source? | ⚠️ Source-available, not fully open source |

---

<div align="center">

```
╔══════════════════════════════════════════════════════════════╗
║                                                              ║
║   By using Godlike-chat, you acknowledge that you have       ║
║   read, understood, and agree to be bound by all terms       ║
║   outlined in this Legal Document.                           ║
║                                                              ║
║   © 2026 Nothing-dot-exe — All Rights Reserved               ║
║                                                              ║
╚══════════════════════════════════════════════════════════════╝
```

**[@Nothing-dot-exe](https://github.com/Nothing-dot-exe) — Godlike-chat v2.0**

</div>
