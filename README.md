# Kiro-on-Windows-Linux
 Phase 1: Get Your Free Kiro Credits
Step 1: Download Kiro IDE
Visit kiro.dev and download the application for your platform.

Step 2: Sign Up & Login
Open Kiro IDE
Create a new account or sign in
✨ You'll automatically receive 500 free credits!
⚠️ Important: Keep Kiro IDE logged in throughout this setup process.

🌐 Phase 2: Set Up Kiro OpenAI Gateway
This gateway creates a local server that translates OpenAI-compatible requests to Kiro's API, allowing you to use your free credits with any OpenAI-compatible tool.

Step 1: Clone the Repository
git clone https://github.com/Jwadow/kiro-openai-gateway.git
cd kiro-openai-gateway
Step 2: Install Dependencies
pip install -r requirements.txt
Step 3: Configure Environment
cp .env.example .env
This command creates a new .env file by copying all the contents from .env.example.

step 4: Uncomment
# KIRO_CREDS_FILE="~/.aws/sso/cache/kiro-auth-token.json" uncomment this line in .env file.

Note: Open the terminal on this directory kiro-openai-gateway where we have all the kiro code base and run this command python main.py.If the server is successfully running so it's means that your .env file is loaded successfully and you don't need to implement step Step 5: Setup Variables to set this 2 environment variable manually KIRO_CREDS_FILE and PROXY_API_KEY.
Step 5: Setup Variables
Before starting the server, you need to set the required environment variables for Kiro credentials and your proxy API key.

Windows (Command Prompt)
:: Set the path to your Kiro credentials JSON file
set KIRO_CREDS_FILE=C:/Users/TechLink/.aws/sso/cache/kiro-auth-token.json

:: Set your super-secret proxy API key
set PROXY_API_KEY=my-super-secret-password-123
⚠ Note: These set commands only last for the current terminal session. If you close the terminal, you will need to set them again.

Linux / Ubuntu (Bash)
Before starting the Kiro Gateway server, set the required environment variables in your terminal:

# Set the path to your Kiro credentials JSON file
export KIRO_CREDS_FILE=~/.aws/sso/cache/kiro-auth-token.json

# Set your super-secret proxy API key
export PROXY_API_KEY=my-super-secret-password-123
⚠ Note: These export commands only last for the current terminal session. To make them permanent, you can add them to your ~/.bashrc or ~/.zshrc.

Step 6: Start the Gateway Server
python main.py
✅ Success Indicator: You should see:

Server running at http://localhost:8000
📌 Note: To check if the gateway is running, open your browser and go to:

http://localhost:8000

You should not use 0.0.0.0 in the browser, as it is only a server binding address.

This site can’t be reached
The webpage at http://0.0.0.0:8000/ might be temporarily down or it may have moved permanently to a new web address.
ERR_ADDRESS_INVALID
You should convert this http://0.0.0.0:8000 url into your localhost by running python main.py --host 127.0.0.1 command in the terminal and close the old one. Then run this on the browser.

http://127.0.0.1:8000/

It'll show something like this: {"status":"ok","message":"Kiro Gateway is running","version":"2.0-rc.1"} so it means that server is running successfully in the localhost.

You should stopped this server once checked it's working or The server must stay running.

🔀 Phase 3: Set Up Claude Code Router
The Claude Code Router wraps the official Claude CLI and redirects requests to your local Kiro gateway.

Step 1: Install Required Packages
npm install -g @anthropic-ai/claude-code
npm install -g @musistudio/claude-code-router
Step 2: Create Configuration File
For windows users:
Open the Start menu, type cmd, and press Enter. This will open the Command Prompt at your root directory.

C:\Users\username
Then open the code editor(IDE) by running this command code .. There you find a .claude-code-router folder in that folder there is an file config.json.

Windows Path: C:\Users\<YourUsername>\.claude-code-router\config.json

You just paste this script in config.json file:

{
  "LOG": true,
  "LOG_LEVEL": "debug",
  "Providers": [
    {
      "name": "kiro",
      "api_base_url": "http://localhost:8000/v1/chat/completions",
      "api_key": "my-super-secret-password-123",
      "models": [
        "claude-sonnet-4-5",
        "claude-haiku-4-5",
        "claude-opus-4-5"
      ],
      "transformer": {
        "use": ["openrouter"]
      }
    }
  ],
  "Router": {
    "default": "kiro,claude-sonnet-4-5",
    "think": "kiro,claude-sonnet-4-5",
    "background": "kiro,claude-sonnet-4-5",
    "longContext": "kiro,claude-sonnet-4-5",
    "webSearch": "kiro,claude-sonnet-4-5"
  }
}
For Linux(ubuntu) users:
Open the ubuntu terminal.

Create or edit the file at: ~/.claude-code-router/config.json by paste the following configuration:

cat > ~/.claude-code-router/config.json << 'EOF'
{
  "LOG": true,
  "LOG_LEVEL": "debug",
  "Providers": [
    {
      "name": "kiro",
      "api_base_url": "http://localhost:8000/v1/chat/completions",
      "api_key": "my-super-secret-password-123",
      "models": [
        "claude-sonnet-4-5",
        "claude-haiku-4-5",
        "claude-opus-4-5"
      ],
      "transformer": {
        "use": ["openrouter"]
      }
    }
  ],
  "Router": {
    "default": "kiro,claude-sonnet-4-5",
    "think": "kiro,claude-sonnet-4-5",
    "background": "kiro,claude-sonnet-4-5",
    "longContext": "kiro,claude-sonnet-4-5",
    "webSearch": "kiro,claude-sonnet-4-5"
  }
}
EOF
Note: Ensure the api_key matches the PROXY_API_KEY you set in Phase 2. The model name claude-sonnet-4-5 corresponds to the models provided by the Kiro Gateway.
Configuration Explained
Key	Description
api_base_url	Points to your local Kiro gateway
api_key	Must match PROXY_API_KEY in your .env file
models	Available Claude models through Kiro
Router	Maps different request types to providers
🚀 Phase 4: Launch & Test
Step 1: Start the Router Service
Open a new terminal and run:

ccr start
It's started the server in the background.

Step 2: Run Claude Code
Instead of the standard claude command, use:

ccr code
Step 3: Test Your Setup
Try a simple prompt:

Hi! Can you confirm you're working?
🎉 Congratulations! You're now using Claude Code with Kiro's free credits!

Step 4: Check Model:
Check which model is running in the background run

ccr model
Click on backgroud model it'll showing the model which is used in the background.

🎯 Bonus: Get 500 More Free Credits with Kiro CLI
Once your IDE credits are exhausted, you can get another 500 free credits by installing Kiro CLI with the same account!

Step 1: Install Kiro CLI
Follow the official installation guide: kiro.dev/docs/cli/installation

Step 2: Login to Kiro CLI
kiro login
Step 3: Update Environment Configuration
Edit your .env file in the kiro-openai-gateway folder:

Remove or comment out:

# KIRO_CREDS_FILE="~/.aws/sso/cache/kiro-auth-token.json"
Add this line:

KIRO_CLI_DB_FILE="~/.local/share/kiro-cli/data.sqlite3"
Step 4: Update the Codebase
Use your IDE's Find and Replace feature:

Find	Replace With
KIRO_CREDS_FILE	KIRO_CLI_DB_FILE
Apply this replacement across the entire kiro-openai-gateway codebase.

Step 5: Restart the Server
python main.py
✅ Your Kiro CLI credits are now active!

🔧 Troubleshooting
Common Issues & Solutions
Issue	Solution
Server not starting	Ensure Python 3.10+ is installed and all dependencies are met
Connection refused	Verify the gateway server is running on port 8000
Authentication errors	Check that api_key matches PROXY_API_KEY in .env
Credits not working	Ensure you're logged into Kiro IDE/CLI
Need Help?
Check the Kiro OpenAI Gateway GitHub for issues
Visit Kiro Documentation for official support
📊 Quick Reference
Terminal Windows Needed
Terminal	Command	Purpose
Terminal 1	python main.py	Kiro Gateway Server
Terminal 2	ccr start	Claude Code Router
Terminal 3	ccr code	Claude Code Interface
Available Models
claude-sonnet-4-5 — Balanced performance
claude-haiku-4-5 — Fast responses
claude-opus-4-5 — Maximum capability
