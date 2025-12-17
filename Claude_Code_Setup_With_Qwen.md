#Claude Code Setup With Qwen – Roman Urdu Simple Guide

Ye guide aapko step-by-step samjhaye gi ke Claude Code ko Alibaba Qwen models ke sath kaise setup karna hai.

#Prerequisites

Setup shuru karne se pehle ye cheezen lazmi hain:

Node.js v18 ya us se upar

PowerShell (Windows ke sath already hoti hai)

#NodeJS_Check

PowerShell open karo aur ye command run karo:

node --version


Agar output mein v18 ya us se zyada ho → ✅ continue karo
Agar nahi ho → Node.js yahan se install karo:

https://nodejs.org

#Step_1_Install_Claude_Code_And_Router

PowerShell open karo aur ye command paste karo:

npm install -g @anthropic-ai/claude-code @musistudio/claude-code-router

#Install_Check
ccr --version


ya

ccr --help


Agar response aa jaye to matlab install theek hai ✅

#Step_2_Install_Qwen_CLI

PowerShell mein ye command run karo:

npm install -g @qwen-code/qwen-code@latest

#Qwen_Check
qwen --version


Agar version show ho jaye → Qwen CLI sahi install ho chuki hai ✅

#Step_3_Qwen_Login

PowerShell mein ye likho:

qwen


Browser open hoga

Login steps follow karo

Login complete hone ke baad PowerShell band mat karo

#Step_4_Find_Qwen_Access_Token

Apne system mein is file ko open karo:

C:\Users\YourUsername\.qwen\oauth_creds.json


YourUsername = aap ka Windows username

Is file ko Notepad mein open karo aur yahan se token copy karo:

"access_token": "PASTE_THIS_TOKEN"


⚠️ Sirf token copy karna hai, quotes ke baghair

#Step_5_Create_Config_Folders

PowerShell mein ye commands run karo:

New-Item -ItemType Directory -Path "$env:USERPROFILE\.claude-code-router" -Force
New-Item -ItemType Directory -Path "$env:USERPROFILE\.claude" -Force


Ye commands required folders create kar dengi.

#Step_6_Create_Router_Config_File

PowerShell mein ye command run karo:

notepad "$env:USERPROFILE\.claude-code-router\config.json"


Notepad open hoga. Us mein neeche diya gaya code paste karo.

⚠️ IMPORTANT
YOUR_QWEN_ACCESS_TOKEN_HERE ki jagah apna real access token paste karo.

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


File Save karo aur Notepad band kar do.

#Step_7_Start_Router

PowerShell mein ye command run karo:

ccr restart


Agar ye message aaye:

Service started successfully


to router sahi chal raha hai ✅

#Step_8_Test_Claude_Code

PowerShell mein likho:

ccr code


Claude Code interface open hoga.
Wahan type karo:

hi


Aur Enter press karo.
Agar reply aa jaye → 🎉 setup successful.

#Troubleshooting
#Command_Not_Found

Node.js check karo

PowerShell close kar ke dobara open karo

#Token_Error

Token dobara check karo

File path sahi ho:

.qwen/oauth_creds.json

#Router_Not_Starting

Port 3456 kisi aur app ke use mein na ho

#Config_File_Issue

Confirm karo file yahan mojood ho:

C:\Users\YourUsername\.claude-code-router\config.json

#Quick_Checklist

 node --version → 18+

 qwen command login working

 Claude Code & Router installed

 Access token config mein added

 ccr restart successful

 ccr code test working

#Follow_On_LinkedIn
https://www.linkedin.com/in/hamza-shakoor-6a4350180/
