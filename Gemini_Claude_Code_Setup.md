# Complete Guide: Using Claude Code with Google Gemini for Free

This comprehensive guide will walk you through setting up Claude Code with Google Gemini models, including detailed explanations for each command and step.

---

## ⭐ Requirements
Before beginning, make sure the following are installed:

* **Node.js v18 or later**
* **PowerShell** (for Windows users) or terminal access (for Linux/Mac)

### Verify Node.js Installation

Open PowerShell and run:

```powershell
node --version
npm --version
```

- If the version is 18.x or higher for Node.js, you're good to continue.
- If not, download and install the latest LTS release from [https://nodejs.org](https://nodejs.org)

---

## 🔑 Step 1: Generate Your Google API Key

You need to create a Google API key to access Gemini models.

### Steps to create your API key:

1. Visit: [https://aistudio.google.com](https://aistudio.google.com)
2. Sign in with your Google account
3. Select **Get API Key** or navigate to the API key section
4. Click **Create API Key**
5. Copy the generated key which will look like:
```
AIzaSy...............
```

### Command Explanation:
- This API key authenticates your requests to Google's Gemini API
- Keep this key secure and don't share it publicly
- The key follows the format: `AIzaSy` followed by a unique identifier

---

## 🧩 Step 2: Install Claude Code and Router

Install Claude Code and the router globally to enable routing requests to Gemini models.

### Command Explanation:
```bash
npm install -g @anthropic-ai/claude-code @musistudio/claude-code-router
```

- `npm`: Node Package Manager - a package manager for JavaScript
- `install`: Command to install packages
- `-g`: Global flag - installs the package globally so it's available system-wide
- `@anthropic-ai/claude-code`: The Claude Code CLI tool
- `@musistudio/claude-code-router`: A router that forwards Claude Code requests to different AI models (in this case, Gemini)
- Both packages are installed globally (`-g`) so they're available system-wide

Run this command in PowerShell (Run as Administrator):

```powershell
npm install -g @anthropic-ai/claude-code @musistudio/claude-code-router
```

### Verify installations:

```powershell
claude --version
ccr version
```

- `claude --version`: Checks if Claude Code CLI is properly installed
- `ccr version`: Checks if Claude Code Router is properly installed
- `ccr` is the shorthand command for Claude Code Router

---

## 📁 Step 3: Create Required Configuration Folders

Create the necessary directories for Claude Code and the router configuration.

### Command Explanation for Windows PowerShell:
```powershell
mkdir $HOME/.claude-code-router
mkdir $HOME/.claude
```

- `mkdir`: Make directory command
- `$HOME`: PowerShell variable representing your home directory (e.g., `C:\Users\YourUsername\` on Windows)
- `/.claude-code-router`: Directory for router configuration files
- `/.claude`: Directory for Claude Code configuration files

On Linux/Mac, the equivalent command is:
```bash
mkdir -p ~/.claude-code-router ~/.claude
```

**Purpose**: These directories store configuration files needed for Claude Code and the router to function properly.

---

## ⚙️ Step 4: Configure Your Environment Variable (API Key)

Set up your Google API key as an environment variable so the router can access it.

### Command Explanation for Windows PowerShell:
```powershell
[System.Environment]::SetEnvironmentVariable('GOOGLE_API_KEY', 'YOUR_API_KEY_HERE', 'User')
```

- `[System.Environment]::SetEnvironmentVariable`: PowerShell command to set environment variables
- `'GOOGLE_API_KEY'`: The name of the environment variable
- `'YOUR_API_KEY_HERE'`: Replace with your actual Google API key from Step 1
- `'User'`: Sets the variable for the current user (not system-wide)

### Example:
```powershell
[System.Environment]::SetEnvironmentVariable('GOOGLE_API_KEY', 'AIzaSyYourActualApiKeyHere', 'User')
```

### Verify the Key

Close PowerShell → open a new window → run:

```powershell
echo $env:GOOGLE_API_KEY
```

- `$env:GOOGLE_API_KEY`: PowerShell syntax to access the environment variable
- If the key appears, the environment variable is configured correctly

**Purpose**: The environment variable allows the router to access your API key without hardcoding it in configuration files.

---

## ⚙️ Step 5: Create the Router Configuration

Create the configuration file that tells the router how to connect to Gemini models.

### For Windows PowerShell users:
Since Windows doesn't support the `cat << EOF` syntax, create the file using Notepad:

```powershell
notepad "$env:USERPROFILE\.claude-code-router\config.json"
```

Then paste this JSON configuration:

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

### Configuration Explanation:

- `"LOG": true` - Enables logging for debugging
- `"LOG_LEVEL": "info"` - Sets logging level to show informational messages
- `"HOST": "127.0.0.1"` - Localhost address where the router will run
- `"PORT": 3456` - Port number where the router will listen for requests
- `"API_TIMEOUT_MS": 600000` - Timeout set to 10 minutes (600,000ms) for long operations
- `"Providers"` - Defines the AI model providers (in this case, Gemini)
- `"api_base_url"`: The base URL for the Gemini API
- `"api_key"`: Uses the environment variable `$GOOGLE_API_KEY`
- `"transformer"`: Configures request/response transformation for Gemini compatibility
- `"Router"` - Maps different Claude Code operations to specific models

### Router Mapping Explanations:
- `"default"`: Used for regular Claude Code commands
- `"background"`: Used for background tasks
- `"think"`: Used for thinking/analysis tasks
- `"longContext"`: Used for tasks requiring long context
- `"webSearch"`: Used for web search functionality

### Gemini Model Options:
- `"gemini-2.5-flash"`: Latest and most capable flash model
- `"gemini-2.0-flash"`: Previous version, still capable but faster

---

## 🚀 Step 6: Validate Installation

Test that all components are properly installed and configured.

### Command Explanation:
```powershell
claude --version
ccr version
echo $env:GOOGLE_API_KEY
```

- `claude --version`: Verifies Claude Code is installed
- `ccr version`: Verifies Claude Code Router is installed
- `echo $env:GOOGLE_API_KEY`: Verifies your API key is accessible as an environment variable

Run these commands in PowerShell:

```powershell
claude --version
ccr version
echo $env:GOOGLE_API_KEY
```

If all commands return output without errors, the setup is successful.

---

## 🚀 Step 7: Start Using Claude Code with Gemini

### Start the Router (Terminal 1)

```powershell
ccr start
```

- `ccr start`: Starts the Claude Code Router service
- Wait until you see: `✔ Service started successfully`

**Purpose**: The router acts as a bridge between Claude Code and the Gemini API, translating Claude Code commands into Gemini-compatible requests.

### Use Claude Code (Terminal 2)

Navigate to your project directory:

```powershell
cd your-project-folder
ccr code
```

- `cd your-project-folder`: Changes to your project directory
- `ccr code`: Launches Claude Code through the router with Gemini backend

---

## 🧪 Step 8: Quick Test

Test your Claude Code setup with Gemini models.

### Command Explanation:
```powershell
ccr code
```

- `ccr code`: Launches Claude Code through the router
- This command starts an interactive Claude Code session using Gemini models

Run this command in PowerShell:

```powershell
ccr code
```

When the Claude interface opens, try:

```
> hi
```

**Purpose**: This tests if Claude Code is properly communicating with the Gemini models through the router.

---

## 🔄 Troubleshooting Common Issues

### 1️⃣ API Key Issues
If you get authentication errors:

1. Verify your API key is correct:
```powershell
echo $env:GOOGLE_API_KEY
```

2. Check that your Google Cloud project has the Gemini API enabled:
   - Visit Google Cloud Console
   - Enable the "Generative Language API"

### 2️⃣ Router Issues
If the router won't start:

1. Check if port 3456 is available:
```powershell
Test-NetConnection -ComputerName localhost -Port 3456
```

2. Restart the router:
```powershell
ccr restart
```

### 3️⃣ Connection Issues
If Claude Code can't connect:

1. Verify the router is running:
```powershell
ccr status
```

2. Check your internet connection and firewall settings

---

## ⚠️ Important Notes

1. **Keep your Google API key secure** - don't share it publicly or commit it to version control
2. **The configuration maps different Claude Code operations** to appropriate Gemini models
3. **Make sure your Google Cloud project has Gemini API enabled** and sufficient quota
4. **The API timeout is set to 10 minutes (600000ms)** to handle longer operations
5. **The router runs on port 3456** - ensure this port is not blocked by firewall
6. **Gemini API usage may incur costs** - monitor your usage in Google Cloud Console

---

## 🔄 Gemini Model Options

You can use different Gemini models based on your needs:

- `gemini-2.5-flash`: Latest and most capable flash model - good for most tasks
- `gemini-2.0-flash`: Previous version, still capable but faster - good for simple tasks

### Changing Models:
To use a different model, change the model name in the router configuration:
- From `"default": "gemini,gemini-2.5-flash"`
- To `"default": "gemini,gemini-2.0-flash"` (for the faster model)

---

## 🛠️ Additional Commands and Tips

### Useful Claude Code Commands:
- `> help` - Show available commands
- `> /file <path>` - Include a file in the conversation
- `> /clear` - Clear the current conversation
- `> /exit` - Exit Claude Code

### Router Management Commands:
- `ccr start` - Start the router
- `ccr stop` - Stop the router
- `ccr restart` - Restart the router
- `ccr status` - Check router status
- `ccr version` - Check router version

### Configuration Updates:
If you need to update your configuration later:
1. Stop the router: `ccr stop`
2. Edit the config file: `notepad "$env:USERPROFILE\.claude-code-router\config.json"`
3. Restart the router: `ccr restart`

---

## 📞 Support and Resources

- Google AI Studio: [https://aistudio.google.com](https://aistudio.google.com)
- Google Gemini API Documentation: [https://ai.google.dev](https://ai.google.dev)
- Claude Code Documentation: [https://docs.anthropic.com](https://docs.anthropic.com)
- Claude Code Router: Check GitHub repository for updates

---
Don't forget to subscribe to the YouTube Channel [Code With Hamza](https://www.youtube.com/@codewithhamza119) for more tutorials and guides.