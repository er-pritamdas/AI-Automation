# 🦞 Running Moltbot (Claude Bot) Locally with Ollama

**Goal**: Run Moltbot / Claude Bot 100% locally without OpenAI, Anthropic, or any paid AI APIs, using Llama 3.x (8B) via Ollama, and connect it to WhatsApp.

![Moltbot Infographics](Images/Moltbolt%20infographics.png)

This guide documents every step, including issues, fixes, and current limitations.

---

## 🧠 System Setup

- **OS**: Linux (Ubuntu)
- **RAM**: 8 GB (Minimum for 8B models)
- **Node.js**: ≥ 24 (Recommended)
- **Package manager**: pnpm ≥ 10
- **LLM runtime**: Ollama
- **Model**: Llama 3.x (8B)
- **Bot framework**: Moltbot / Clawdbot
- **Channel**: WhatsApp (personal)

---

## 1️⃣ Install & Upgrade Node.js (Required)

Moltbot requires Node ≥ 22, but Node 24+ is strongly recommended for best performance and compatibility.

### Install NVM (Node Version Manager)

```bash
curl -fsSL https://raw.githubusercontent.com/nvm-sh/nvm/v0.39.7/install.sh | bash
source ~/.bashrc
```

### Install Node 24

```bash
nvm install 24
nvm use 24
nvm alias default 24
```

**Verify:**

```bash
node -v
```

---

## 2️⃣ Install pnpm (Correct Way)

`pnpm` is required for Moltbot development workflows.

```bash
corepack enable
corepack prepare pnpm@latest --activate
pnpm setup
source ~/.bashrc
```

**Verify:**

```bash
pnpm -v
```

---

## 3️⃣ Install Ollama (Local LLM Runtime)

Ollama allows us to run LLMs locally.

```bash
curl -fsSL https://ollama.com/install.sh | sh
```

**Verify:**

```bash
ollama --version
```

---

## 4️⃣ Pull Local LLM Model (8B – Laptop Friendly)

We will use Llama 3.1 8B, which is efficient enough for 8GB RAM laptops.

```bash
ollama pull llama3.1:8b
```

![Pulling Llama 3.1 8B Model](Images/Ollama%20llama318b.png)

**Test the model:**

```bash
ollama run llama3.1:8b
```

![Test Run of Llama Model](Images/Working%20llama%20Model%20Locally.png)

---

## 5️⃣ Install Clawdbot / Moltbot CLI

⚠️ **Important**: Do not install via global `pnpm`/`npm`. Use `npx` or the official installer to avoid path issues.

```bash
npx moltbot --version
# or
npx clawdbot --version
```

![Moltbot Installation](Images/Moltbot%20Installation.png)

---

## 6️⃣ Initialize Moltbot / Clawdbot

Initialize the bot configuration.

```bash
clawdbot configure
```

![Moltbot Installation Process](Images/Moltbot%20installation%20Process.png)

**Configuration Choices:**

- **Mode**: Local
- **Skip paid AI providers** (We will configure Ollama manually later)
- **Skip models for now**
- **Skip channels initially**

This creates:

- `~/.clawdbot/clawdbot.json`
- `~/.clawdbot/agents/main/`

---

## 7️⃣ Configure Ollama as a Model Provider (UI)

Start the Moltbot Gateway to access the UI:

```bash
clawdbot gateway
```

**Open Control UI**: [http://127.0.0.1:18789/](http://127.0.0.1:18789/)

![Moltbot Landing Page](Images/Moltbot%20Landing%20Page.png)

### Add Custom Provider

Go to **Providers** configuration:

1.  **Provider ID**: `custom-1`
2.  **Base URL**: `http://127.0.0.1:11434` (Default Ollama port)
3.  **Auth**: `api-key`
4.  **API Key**: `local` (Dummy value, not verified by Ollama)

### Add Model to Provider

1.  **Model ID**: `llama3.1`
2.  **Name**: `llama3.1 (local)`
3.  **Context Window**: `16000`
4.  **Max Tokens**: `1024`
5.  **Supports Developer Role**: ✅

![Custom Providers in Moltbot](Images/Custom%20providers%20in%20Moltbot.png)

Apply changes.

![Moltbot UI Connected](Images/Moltbot%20UI%20Connected.png)

---

## 8️⃣ Set Default Model (IMPORTANT)

The UI currently does not allow setting default models cleanly for custom providers. This must be done manually in the config file.

**Edit config:**

```bash
nano ~/.clawdbot/clawdbot.json
```

**Set defaults:**

```json
"agents": {
  "defaults": {
    "model": {
      "primary": "custom-1/llama3.1"
    }
  }
}
```

❌ **Remove** any references like `"ollama/llama3.1"` if they exist from auto-detection.

**Restart gateway:**

```bash
clawdbot gateway stop
clawdbot gateway
```

![Moltbot Gateway Running](Images/Moltbot%20Running.png)
![Clawdbot Running Logs](Images/Clawdbot%20Running%20Logs.png)

**Verify models:**

```bash
clawdbot models status --json
```

---

## 9️⃣ WhatsApp Channel Setup

Clawdbot supports personal WhatsApp login.

1.  Run configure:
    ```bash
    clawdbot configure
    ```
2.  Enable **WhatsApp**.
3.  Scan the QR code that appears in the terminal.

![Connecting Whatsapp with Moltbot](Images/Connecting%20Whatsapp%20with%20Moltbot.png)

Keep the gateway running. You should see logs confirming connection:

```
[whatsapp] Listening for personal WhatsApp inbound messages.
```

---

## 🔟 Understanding Commands & Limitations

### ❌ Agent Command (`clawdbot agent ...`)

Currently **BROKEN** with Ollama. It crashes due to a streaming adapter bug in Clawdbot where it expects a cloud-style streaming response that the local Ollama adapter handles differently.

### ❌ Message Send Without Channel

Fails unless a channel is configured.

### 🔴 Critical Limitation: Agent Mode

- **Error**: `Unhandled API in mapOptionsForApi`
- **Cause**: Agent loop always uses streaming, and the Ollama streaming adapter is incomplete.
- **Impact**:
  - `clawdbot agent` fails.
  - WhatsApp inbound messages capable of triggering the agent will crash it.
  - Web UI chat works for basic completion but fails on full agentic loops.

---

## 🏁 Summary of Working Features

| Feature                | Status            |
| :--------------------- | :---------------- |
| Ollama local inference | ✅                |
| Model resolution       | ✅                |
| Gateway                | ✅                |
| WhatsApp connection    | ✅                |
| Agent mode             | ❌ (upstream bug) |
| Streaming              | ❌                |
| Paid APIs              | ❌ (not used)     |

**Key Takeaway**: This setup creates a fully local, cost-free setup. While the autonomous "Agent" mode currently has a bug with local streaming, the foundational connection between WhatsApp, Moltbot, and Ollama is functional. Once the streaming adapter is patched, this setup will be fully autonomous.
