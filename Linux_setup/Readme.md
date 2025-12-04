🚀 Complete WSL (Ubuntu) Developer Environment Setup
With Gemini CLI, Claude CLI, CLAUDE-CODE-ROUTER, Node.js, Python, Git, and More

This guide explains every step clearly and simply so you can set up a complete AI-development environment on Ubuntu running inside WSL (Windows Subsystem for Linux).

Perfect for working with:

Gemini CLI

Claude CLI

Context7

MCP tools

Node.js / Python development

Local AI routing

🧩 1. Install Ubuntu for WSL

Download the WSL Ubuntu installer:

🔗 https://releases.ubuntu.com/noble/ubuntu-24.04.3-wsl-amd64.wsl

Run it → It installs Ubuntu as a separate Linux environment inside Windows.

Then:

Choose a username

Choose a password
(Note: it will NOT be visible when typing — this is normal.)

🧰 2. Update System (VERY IMPORTANT)
sudo apt update && sudo apt upgrade -y

🛠️ 3. Install Core Tools
A. Install Git
sudo apt install git -y

B. Install Build Tools (required for many npm packages)
sudo apt install build-essential -y

🐍 4. Install Python + Pip + Venv
sudo apt install python3 python3-pip python3-venv -y


You can create virtual environments later if needed.

🟦 5. Install Node.js (Required for Gemini, Claude, MCP)

Install Node.js LTS 22.x:

curl -fsSL https://deb.nodesource.com/setup_22.x | sudo -E bash -
sudo apt install -y nodejs


Verify:

node -v
npm -v

📦 6. Fix NPM Permission Issues (Recommended)

This prevents global install errors like EACCES (permission denied).

Step 1: Create a safe directory
mkdir ~/.npm-global

Step 2: Tell npm to use it
npm config set prefix ~/.npm-global

Step 3: Add to PATH
echo 'export PATH="$HOME/.npm-global/bin:$PATH"' >> ~/.bashrc
source ~/.bashrc


Now install global packages safely:

npm install -g pnpm

🟪 7. Install PNPM (Recommended for Node Projects)
npm install -g pnpm

🌟 8. Install Gemini CLI
npm install -g @google/gemini-cli


Login:

gemini login


Initialize project config:

gemini init

🤖 9. Install Claude CLI
npm install -g claude-code


Login:

claude login

🔌 10. Install Claude-Code-Router (Router to Use Gemini with Claude CLI)
npm install -g @anthropic-ai/claude-code @musistudio/claude-code-router


Create config folders:

mkdir -p ~/.claude-code-router ~/.claude

Create config file:
cat > ~/.claude-code-router/config.json << 'EOF'
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
      "api_key": "PASTE_YOUR_GEMINI_API_KEY_HERE",
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
    "longContextThreshold": 60000
  }
}
EOF


❗ IMPORTANT:
Environment variables inside JSON (like "api_key": "$GOOGLE_API_KEY") do NOT work.
You MUST paste the actual Gemini API key into "api_key".

▶️ 11. Start the Router
ccr start


If you see:

✅ Service is already running in the background.


→ Your router is running successfully.

Now Claude CLI will use Gemini models through the router.

🤝 12. Use Claude with Gemini

Open a new terminal:

claude chat


Type:

Hello


If the router is running → Claude responds using Gemini 2.5 Flash.

🔧 13. Install Useful Utilities
A. curl + wget
sudo apt install curl wget -y

B. unzip
sudo apt install unzip -y

C. jq
sudo apt install jq -y

💻 14. Install VS Code (Optional)
sudo snap install code --classic

⚙️ 15. Optional: Improve Your .bashrc

Edit:

nano ~/.bashrc


Add shortcuts:

alias ll='ls -lah'
alias g='git'
alias venv="python3 -m venv venv"


Apply:

source ~/.bashrc

🎉 16. Your Linux Development Environment Is Ready

From now on, simply search “WSL” or “Ubuntu” in Windows and use the Linux terminal normally.

You can now run:

gemini chat → Gemini chat

claude chat → Claude using Gemini API

ccr start → Router

Node, Python, Git, MCP tools, everything works smoothly.