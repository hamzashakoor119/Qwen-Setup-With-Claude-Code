# Claude Code Setup With Qwen - Roman Urdu Simple Guide

Ye guide aapko step by step samjhaye gi ke Claude Code ko
Alibaba Qwen models ke sath kaise setup karna hai.

## Prerequisites

Setup shuru karne se pehle ye cheezen lazmi hain:

- Node.js v18 ya us se upar
- PowerShell (Windows ke sath already hoti hai)
arduino
### Node.js Version Check

PowerShell open karo aur ye command run karo:

```
node --version
```

Agar output mein v18 ya us se zyada ho to continue karo.
Agar nahi ho to Node.js yahan se install karo:
https://nodejs.org
bash
Copy code
## Step 1: Claude Code aur Router Install karo

PowerShell open karo aur ye command paste karo:

npm install -g @anthropic-ai/claude-code @musistudio/claude-code-router
sql
Copy code
Install check karne ke liye:

ccr --version
ya
ccr --help

Agar command chal jaye to matlab install successful hai.
graphql
Copy code
## Step 2: Qwen CLI Install karo

PowerShell mein ye command run karo:

npm install -g @qwen-code/qwen-code@latest
sql
Copy code
Qwen install check:

qwen --version
arduino
Copy code
## Step 3: Qwen Login

PowerShell mein ye command run karo:

qwen

Browser open hoga.
Login steps follow karo.
Login complete hone ke baad PowerShell band mat karo.
makefile
Copy code
## Step 4: Qwen Access Token Find karo

Is file ko open karo:

C:\Users\YourUsername\.qwen\oauth_creds.json

YourUsername ki jagah apna Windows username hoga.
sql
Copy code
Is file ko Notepad mein open karo aur yahan se token copy karo:

"access_token": "YAHAN_WALA_TOKEN"

Sirf token copy karo, quotes ke baghair.
php
Copy code
## Step 5: Config Folders Create karo

PowerShell mein ye commands run karo:

New-Item -ItemType Directory -Path "$env:USERPROFILE\.claude-code-router" -Force
New-Item -ItemType Directory -Path "$env:USERPROFILE\.claude" -Force
nginx
Copy code
## Step 6: Router Config File Create karo

PowerShell mein ye command run karo:

notepad "$env:USERPROFILE\.claude-code-router\config.json"
bash
Copy code
Notepad open hoga.
Neeche diya gaya code paste karo.

IMPORTANT:
YOUR_QWEN_ACCESS_TOKEN_HERE ki jagah apna real token paste karo.
json
Copy code
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
arduino
Copy code
File save karo aur Notepad band kar do.
yaml
Copy code
## Step 7: Router Start karo

PowerShell mein ye command run karo:

ccr restart

Agar ye message aaye:
Service started successfully

To matlab router sahi chal raha hai.
graphql
Copy code
## Step 8: Claude Code Test karo

PowerShell mein likho:

ccr code

Claude Code interface open hoga.
Wahan type karo:

hi

Aur Enter press karo.
Agar reply aa jaye to setup successful hai.
yaml
Copy code
## Troubleshooting

Command not found:
Node.js install check karo
PowerShell dobara open karo

Token error:
Token dobara check karo
.qwen/oauth_creds.json file verify karo

Router start nahi hota:
Port 3456 kisi aur app ke use mein na ho

Config file issue:
Confirm karo file yahan mojood ho:
C:\Users\YourUsername\.claude-code-router\config.json
bash
Copy code
## Quick Checklist

node --version (18+)
qwen command working
Claude Code & Router installed
Access token added
ccr restart successful
ccr code test working
ruby
Copy code
## Follow On LinkedIn

https://www.linkedin.com/in/hamza-shakoor-6a4350180/
