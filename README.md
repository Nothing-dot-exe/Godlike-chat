# 🤖 NVIDIA NEXT — Premium AI Intelligence Suite

![NVIDIA NEXT](https://img.shields.io/badge/NVIDIA-NIM-green?style=for-the-badge&logo=nvidia)
![Next.js](https://img.shields.io/badge/Next.js-15-black?style=for-the-badge&logo=next.js)
![React](https://img.shields.io/badge/React-19-61DAFB?style=for-the-badge&logo=react)
![Status](https://img.shields.io/badge/Status-Ultra--Premium-gold?style=for-the-badge)

**NVIDIA NEXT** is a high-performance, long-term memory-capable AI chatbot built on the NVIDIA NIM infrastructure. It transforms standard LLM interactions into a personalized, visual, and uncensored experience.

---

## ✨ Key Features

### 🧠 Long-Term Memory (Persistent Intelligence)
The bot doesn't just chat; it learns. Every 4 messages, the system automatically extracts facts about you (preferences, name, habits) and stores them in your local **Memory Vault**. These facts are injected into every future conversation, ensuring the AI never forgets who you are.

### 🔓 Uncensored Mode
Toggle the "Uncensored" switch to bypass standard guardrails. This mode uses custom prompt injection and a high-temperature (0.9) configuration to provide raw, creative, and unrestrained responses.

### 🖥️ Visual Code Sandbox
Built-in **Interactive Web Runtime**. When the AI generates HTML/CSS/JS code, you can click **"Preview UI"** to run the application instantly in a secure sandbox directly inside the chat bubble.

### 🌐 Web Context Reader
Paste any URL (news, wiki, docs) into the chat. The backend uses a stealth scraper to strip away ads and noise, feeding the raw article text directly to the AI for instant summarization and analysis.

### 🛡️ Security & Privacy
*   **PIN Lock:** Secure your entire chat history with a SHA-256 hashed 4-digit PIN.
*   **Panic Button:** One-click instant wipe of all local storage data.
*   **Local-First:** All memories and chats stay in your browser. Nothing is stored on our servers.

---
## 🛠️ How it was Built

### The Tech Stack
*   **Frontend:** [Next.js 15 (App Router)](https://nextjs.org/) & [React 19](https://react.dev/) for a lightning-fast, state-of-the-art interface.
*   **Styling:** Custom **Cyber-Fluid CSS** with glassmorphism, live particle backgrounds, and dynamic theme switching.
*   **AI Engine:** [NVIDIA NIM SDK](https://build.nvidia.com/explore/discover) (OpenAI-compatible) using models like `Llama 3.1 70B` and `Mixtral 8x7B`.
*   **Backend:** Next.js Edge Functions for API handling and `Cheerio` for high-speed web scraping.

### Development Journey
This project was engineered to push the limits of what a "simple chatbot" can do. We integrated **AbortControllers** for real-time stream stopping, implemented **Debounced LocalStorage syncing** to handle high-speed data, and built a custom **Memory Extraction Pipeline** that runs asynchronously in the background.

---

## 🎨 Personalization
Go to **Settings** (⚙️) to customize:
*   **Themes:** Switch between 6 premium themes (Cyberpunk, Midnight, Ghost, etc.).
*   **Avatars:** Upload your own image or choose from a library of custom AI personas.
*   **Layout:** Adjust font scales, live backgrounds, and model parameters on the fly.

---

> [!TIP]
> Use the **Stop Button** (⏹️) during a long generation to instantly interrupt the AI and save tokens!

---

