# Claude Code Setup With Gemini - Simple Guide for Beginners

This guide will help you set up Claude Code to work with Google's Gemini models. Follow these simple steps:

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

### Step 1: Get Your Google API Key
1. Go to [https://aistudio.google.com](https://aistudio.google.com)
2. Sign in with your Google account
3. Click **Get API Key** or **Generate API Key**
4. Copy the generated key (starts with `AIzaSy...`)

### Step 2: Install Claude Code and Router
In PowerShell, run:
```
npm install -g @anthropic-ai/claude-code @musistudio/claude-code-router
```

### Step 3: Set API Key as Environment Variable
In PowerShell, run (replace YOUR_API_KEY_HERE with your actual API key from Step 1):
```
[System.Environment]::SetEnvironmentVariable('GOOGLE_API_KEY', 'YOUR_API_KEY_HERE', 'User')
```

### Step 4: Create Config Folders
In PowerShell, run:
```
New-Item -ItemType Directory -Path "$env:USERPROFILE\.claude-code-router" -Force
New-Item -ItemType Directory -Path "$env:USERPROFILE\.claude" -Force
```

### Step 5: Create Router Configuration
In PowerShell, run:
```
notepad "$env:USERPROFILE\.claude-code-router\config.json"
```

Copy and paste this text into the file that opens:
```json
{
  "LOG": true,
  "LOG_LEVEL": "info",
  "HOST": "127.0.0.1",
  "PORT": 3456,
  "API_TIMEOUT_MS": 600000,
  "Providers": [
    {
      "name": "gemini",
      "api_base_url": "https://generativelanguage.googleapis.com/v1beta/models/",
      "api_key": "$GOOGLE_API_KEY",
      "models": [
        "gemini-2.5-flash",
        "gemini-2.0-flash"
      ],
      "transformer": {
        "use": ["gemini"]
      }
    }
  ],
  "Router": {
    "default": "gemini,gemini-2.5-flash",
    "background": "gemini,gemini-2.5-flash",
    "think": "gemini,gemini-2.5-flash",
    "longContext": "gemini,gemini-2.5-flash",
    "longContextThreshold": 60000,
    "webSearch": "gemini,gemini-2.5-flash"
  }
}
```

### Step 6: Start the Router
In PowerShell, run:
```
ccr restart
```
Wait until you see "Service started successfully"

### Step 7: Test Claude Code
In PowerShell, run:
```
ccr code
```
When the interface opens, type `hi` and press Enter to test.

## Troubleshooting

If you have problems:

1. **"Command not found" errors**: Make sure Node.js is installed and reopen PowerShell after installing packages
2. **API Key errors**: Double-check you copied the API key correctly and set the environment variable properly
3. **Router won't start**: Make sure port 3456 is not used by another program
4. **Config file not found**: Make sure you created the config.json file in the correct location

## Quick Checklist

- [ ] Node.js installed (`node --version` shows 18 or higher)
- [ ] Claude Code and Router installed
- [ ] Google API key set as environment variable
- [ ] Config file created
- [ ] Router started successfully (`ccr restart`)
- [ ] Test works (`ccr code` then type `hi`)