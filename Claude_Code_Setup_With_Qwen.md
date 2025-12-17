# Claude Code Setup With Qwen

Ye guide aapko step by step samjhaye gi ke Claude Code ko
Alibaba Qwen models ke sath kaise setup karna hai.

## Prerequisites

Setup shuru karne se pehle ye cheezen lazmi hain:

- Node.js v18 ya us se upar
- PowerShell (Windows ke sath already hoti hai)
- 
### Node.js Version Check

```
node --version
```

Agar output mein v18 ya us se zyada ho to continue karo.
Agar nahi ho to Node.js yahan se install karo:
https://nodejs.org

## Step 1: Claude Code aur Router Install karo
Claude Code Setup Or Configration Ky Liaye Har Baar PowerShell Window Directory Py hi Open Krna Hai , Keyboard Sy Window Ka Button press Kry Or Powershell Likhy.
PowerShell open karo aur ye command run karo:

```
npm install -g @anthropic-ai/claude-code @musistudio/claude-code-router
```
Install check karne ke liye:

```
ccr --version
ya
ccr --help
```

Agar command chal jaye to matlab install successful hai.

## Step 2: Qwen CLI Install karo

PowerShell mein ye command run karo:

```
npm install -g @qwen-code/qwen-code@latest
```
Qwen install check:

```
qwen --version
```

## Step 3:Configration Ky Liaye
New PowerShell Open Kro Or Yee Command Runn Kro:

```
code .
```
VS Code Open Hoga Waha yee folder find kro root directory main " .claude-code-router " ugr mill jaye too good nhi mily to manully ctreate kroo.
Root directory main 1 folder create kroo " .claude-code-route " ky name sy then us main 1 file create kroo " config.json " is file main yee code paste kro or save kroo"

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

PowerShell mein ye command run karo:
```
qwen
```

Browser open hoga.
Login steps follow karo.
Login complete hone ke baad PowerShell band mat karo.

## Step 5: Qwen Access Token Find karo

Rot Directory main 1 folder find kroo " .qwen " ky name sy hoga usy open kroo us main 1 file hogi " oauth_creds.json " us file ko open kroo or waha sy access token copy kroo or " .claude-code-router " main " config.json " file main "api_key" ki gaha yee access tokrn paste kro or save kro :

## Step 6: Router Start karo

PowerShell mein ye command run karo:

```
ccr restart
```

Agar ye message aaye:
Service started successfully

To matlab router sahi chal raha hai.

## Step 7: Claude Code Test karo

PowerShell mein likho:

```
ccr code
```

Claude Code interface open hoga.
Wahan type karo:

```
hi
```

Aur Enter press karo.
Agar reply aa jaye to setup successful hai.

## Step 8: Move On Your Project
Apny Project Main aaky new terminal open kry or type kry " ccr code " ugr service ka error dyy too type kry " ccr restart : or service successful hony ky baad type kry " ccr code " ugr claude open hoo jaye too pehly usy hi/hellow kr ky chek kry ugr responce dy raha hai too apna kaam start kr dain .

# Note :
Ugr Start main hi yaa use krty hoye yaaa api ka error aye yaa api ,token limits etc ka error aye too " . qwen " ka folder delete kr ky Step #4 sy Step #7 Tak Steps dubara follow kro issue resolve hoo jaye ga.
Ugr aap ka Setup Oky Chal Raha hai Too Window Directory Py Kisi Bhi terminal main " qwen " ki command run mat krna nhi totoken refresh hoo jaye gaa , new token aajaye gaa or aap ko dubara token copy past krna pry ga .
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

```
C:\Users\YourUsername\.claude-code-router\config.json
```

## Quick Checklist

node --version (18+)
qwen command working
Claude Code & Router installed
Access token added
ccr restart successful
ccr code test working

## Follow On LinkedIn

https://www.linkedin.com/in/hamza-shakoor-6a4350180/
