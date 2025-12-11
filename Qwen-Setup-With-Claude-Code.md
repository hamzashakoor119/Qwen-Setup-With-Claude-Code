# How to Use Claude Code with Qwen Models for Free

## ⭐ Requirements  
Before beginning, make sure the following are installed:

- **Qwen CLI** (installed and authenticated)  
- **Node.js v18 or later**

---

## 🧩 Qwen CLI Installation  
Install the latest Qwen Code CLI:

```bash
npm install -g @qwen-code/qwen-code@latest
```

Verify the installation:

```bash
qwen --version
```

---

## 🚀 Step 1: Install Claude Code Router  
Install Claude Code and the router globally:

```bash
npm install -g @anthropic-ai/claude-code @musistudio/claude-code-router
```

---

## 🔑 Step 2: Get Your Qwen Access Token  

```
C:\Users\PC_USER\.qwen\oauth_creds.json
```
You will see something like this:

```json
{
  "access_token": "YOUR_QWEN_ACCESS_TOKEN_HERE",
  "token_type": "Bearer",
  "refresh_token": "YOUR_QWEN_REFRESH_TOKEN_HERE",
  "resource_url": "portal.qwen.ai",
  "expiry_date": 1764876220290
}
```

Copy your **access_token** — you’ll add it to the router config.

---

## 📁 Step 3: Create Required Folders  
Run inside your WSL terminal:

```bash
mkdir -p ~/.claude-code-router ~/.claude
```

---

## ⚙️ Step 4: Create the Router Configuration  
Paste this to generate the config file:

```bash
cat > ~/.claude-code-router/config.json << 'EOF'

{  
  "LOG": true,  
  "LOG_LEVEL": "info",  
  "HOST": "127.0.0.1",  
  "PORT": 3456,  
  "API_TIMEOUT_MS": 600000,  
  "Providers": [  
    {  
      "name": "qwen",  
      "api_base_url": "https://portal.qwen.ai/v1/chat/completions",  
      "api_key": "YOUR_QWEN_ACCESS_TOKEN_HERE",  
      "models": [  
        "qwen3-coder-plus",  
        "qwen3-coder-plus",  
        "qwen3-coder-plus"  
      ]  
    }  
  ],  
  "Router": {  
    "default": "qwen,qwen3-coder-plus",  
    "background": "qwen,qwen3-coder-plus",  
    "think": "qwen,qwen3-coder-plus",  
    "longContext": "qwen,qwen3-coder-plus",  
    "longContextThreshold": 60000,  
    "webSearch": "qwen,qwen3-coder-plus"  
  }  
}

EOF
```

---

## ▶️ Step 5: Start Using Claude Code with Qwen  
Restart the router:

```bash
ccr restart
```

Launch Claude Code with Qwen support:

```bash
ccr code
```

Test:

```
> hi
```

---

## 🔄 Handling 401 Token Errors  
If your Qwen OAuth token expires:

### 1️⃣ Reauthenticate  
If tokens don’t match, delete `oauth_creds.json` and run:

```bash
qwen
```

### 2️⃣ Update your router config  
```powershell
notepad "$env:USERPROFILE\.claude-code-router\config.json"
```

Replace `api_key` with the new `access_token`.

### 3️⃣ Restart the router  
```bash
ccr restart
```

PowerShell users: ensure your shell environment is correctly set.
