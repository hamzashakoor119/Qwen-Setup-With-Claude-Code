# Claude Code Setup With Qwen

This guide will explain step by step how to set up Claude Code
with Alibaba Qwen models.

# Prerequisites

Before starting the setup, the following things are required:

Node.js v18 or above

PowerShell (already available with Windows)

Node.js Version Check
node --version


If the output shows v18 or above, continue.
If not, install Node.js from here:
https://nodejs.org

## Step 1: Install Claude Code and Router

For Claude Code setup or configuration, every time you must open the PowerShell window in the directory.
Press the Windows key on the keyboard and type PowerShell.
Open PowerShell and run the following command:

```
npm install -g @anthropic-ai/claude-code @musistudio/claude-code-router
```


To check installation:

```
ccr --version
or
ccr --help
```


If the command runs successfully, it means the installation was successful.

## Step 2: Install Qwen CLI

Run this command in PowerShell:

```
npm install -g @qwen-code/qwen-code@latest
```


Check Qwen installation:

```
qwen --version
```

## Step 3: For Configuration

Open a new PowerShell and run this command:

```
code .
```


VS Code will open. Find the folder in the root directory named ".claude-code-router".
If it exists, that’s good. If not, create it manually.

In the root directory, create one folder named ".claude-code-route" and inside it create one file named "config.json".
Paste the following code into this file and save it.

```
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
}
```

## Step 4: Qwen Login

Run this command in PowerShell:

```
qwen
```


A browser will open.
Follow the login steps.
After login is complete, do not close PowerShell.

## Step 5: Find Qwen Access Token

In the root directory, find a folder named ".qwen".
Open it and inside you will find a file named "oauth_creds.json".
Open this file and copy the access token from there, then paste it in the "api_key" field inside the ".claude-code-router" → "config.json" file and save it.

## Step 6: Start Router

Run this command in PowerShell:

```
ccr restart
```


If you see this message:
Service started successfully

It means the router is working correctly.

## Step 7: Test Claude Code

In PowerShell, type:

```
ccr code
```


Claude Code interface will open.
Type:

```
Hy/Hello
```


And press Enter.
If you receive a reply, the setup is successful.

## Step 8: Move On Your Project

Go to your project, open a new terminal and type "ccr code".
If a service error appears, type "ccr restart".
After the service starts successfully, type "ccr code" again.
If Claude opens, first say hi/hello to check.
If it responds, then start your work.

# Note :

If at the start or while using it you get an API error or API/token limits error, then delete the ".qwen" folder and follow Steps #4 to Step #7 again. The issue will be resolved.
If your setup is working fine, then do not run the "qwen" command in any terminal in the Windows directory, otherwise the token will refresh, a new token will be generated, and you will have to copy-paste the token again.

## Troubleshooting

Command not found:
Check Node.js installation
Open PowerShell again

Token error:
Check the token again

Verify .qwen/oauth_creds.json file

Router does not start:
Make sure port 3456 is not being used by another app

Config file issue:
Confirm the file exists here:

C:\Users\YourUsername\.claude-code-router\config.json

Quick Checklist

node --version (18+)
qwen command working
Claude Code & Router installed
Access token added
ccr restart successful
ccr code test working

# Follow On LinkedIn "

https://www.linkedin.com/in/hamza-shakoor-6a4350180/
