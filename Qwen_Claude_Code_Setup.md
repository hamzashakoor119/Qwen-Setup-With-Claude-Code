# How to Use Claude Code with Qwen Models for Free

## ⭐ Requirements
Before beginning, make sure the following are installed:

* **Qwen CLI** (installed and authenticated)
* **Node.js v18 or later**

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

## 🧩 Claude Code Router Installation
Install Claude Code and the router globally:

```bash
npm install -g @anthropic-ai/claude-code @musistudio/claude-code-router
```

---

## 🔑 Step 2: Get Your Qwen Access Token

Find your access token in:
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

Copy your **access_token** — you'll add it to the router config.

---

## 📁 Step 3: Create Required Folders
Run inside your terminal:

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
        "qwen3-coder-max",
        "qwen3-coder-turbo"
      ]
    }
  ],
  "Router": {
    "default": "qwen,qwen3-coder-plus",
    "background": "qwen,qwen3-coder-plus",
    "think": "qwen,qwen3-coder-plus",
    "longContext": "qwen,qwen3-coder-plus",
    "longContextThreshold": 60000
  }
}
EOF
```

## 🚀 Step 5: Start the Router
Start the Claude Code router:

```bash
claude-code-router
```

## 🧪 Step 6: Test the Setup
Test your Claude Code setup with the Qwen backend:

```bash
claude-code --help
```

---

## ⚠️ Notes

1. Replace `YOUR_QWEN_ACCESS_TOKEN_HERE` with your actual access token from the oauth_creds.json file
2. The configuration maps different Claude Code operations to appropriate Qwen models
3. Make sure your Qwen account has sufficient credits/usage allowance
4. The API timeout is set to 10 minutes (600000ms) to handle longer operations

## 🔄 Alternative Models

You can use different Qwen models based on your needs:
- `qwen3-coder-plus`: Good balance of capability and speed
- `qwen3-coder-max`: Most capable for complex tasks
- `qwen3-coder-turbo`: Fastest for simple tasks
