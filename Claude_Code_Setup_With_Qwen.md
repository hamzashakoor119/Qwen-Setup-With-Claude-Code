# Claude Code Setup With Qwen - Simple Guide for Beginners

This guide will help you set up Claude Code to work with Alibaba's Qwen models. Follow these simple steps:

## Prerequisites

Before beginning, make sure you have:

* **Node.js v18 or later** installed
* **PowerShell** (comes with Windows)

Check if Node.js is installed by opening PowerShell and running:
```
node --version
```
If version is 18 or higher, continue. Otherwise, download from [https://nodejs.org](https://nodejs.org)

## Setup Steps

### Step 1: Install Claude Code and Router
Open PowerShell, Run This Command:
```
npm install -g @anthropic-ai/claude-code @musistudio/claude-code-router
```
Chek if it Installed :
```
ccr --version
or
ccr --help
```

### Step 2: Install Qwen CLI
In PowerShell, Run This Command:
```
npm install -g @qwen-code/qwen-code@latest
```
Chek if it Installed :
```
qwen --version
```

### Step 3: Login to Qwen
In PowerShell, run:
```
qwen
```
Follow the login steps in your browser.


```

### Step 4: Find Your Qwen Access Token
Look for this file on your computer:
```
C:\Users\YourUsername\.qwen\oauth_creds.json
```
Open it with Notepad and copy the text after `"access_token": "` (without the quotes).

### Step 5: Create Config Folders
In PowerShell, run:
```
New-Item -ItemType Directory -Path "$env:USERPROFILE\.claude-code-router" -Force
New-Item -ItemType Directory -Path "$env:USERPROFILE\.claude" -Force
```

### Step 6: Create Router Configuration
In PowerShell, run:
```
notepad "$env:USERPROFILE\.claude-code-router\config.json"
```

Copy and paste this text into the file that opens. **Replace `YOUR_QWEN_ACCESS_TOKEN_HERE` with your actual access token from Step 4**:

```json
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
    "longContextThreshold": 60000,
    "webSearch": "qwen,qwen3-coder-plus"
  }
}```

### Step 7: Start the Router
In PowerShell, run:
```
ccr restart
```
Wait until you see "Service started successfully"

### Step 8: Test Claude Code
In PowerShell, run:
```
ccr code
```
When the interface opens, type `hi` and press Enter to test.

## Troubleshooting

If you have problems:

1. **"Command not found" errors**: Make sure Node.js is installed and reopen PowerShell after installing packages
2. **Token errors**: Double-check you copied the access token correctly from the .qwen/oauth_creds.json file
3. **Router won't start**: Make sure port 3456 is not used by another program
4. **Config file not found**: Make sure you created the config.json file in the correct location

## Quick Checklist

- [ ] Node.js installed (`node --version` shows 18 or higher)
- [ ] Qwen CLI installed and logged in (`qwen` command works)
- [ ] Claude Code and Router installed
- [ ] Config file created with your access token
- [ ] Router started successfully (`ccr restart`)
- [ ] Test works (`ccr code` then type `hi`)

 #Follow On Linkedln :
 https://www.linkedin.com/in/hamza-shakoor-6a4350180/
