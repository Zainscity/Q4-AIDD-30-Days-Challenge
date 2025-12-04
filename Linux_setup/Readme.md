🚀 Ubuntu (WSL) Full Environment Setup
Gemini CLI • Claude CLI • Context7 MCP • Node.js • Python • VS Code

This guide explains how to set up a clean development environment inside Ubuntu WSL for AI tools like Gemini CLI, Claude CLI, OpenAI, Context7, and more.

🧩 1. Install Ubuntu (WSL)

Download Ubuntu WSL:

👉 https://releases.ubuntu.com/noble/ubuntu-24.04.3-wsl-amd64.wsl

Install it, launch it, and create:

Username

Password (it will NOT appear while typing — type normally)

🧰 STEP-BY-STEP ENVIRONMENT SETUP (Fresh Ubuntu)

Follow the steps exactly in this order.

2️⃣ Update System (VERY IMPORTANT)
sudo apt update && sudo apt upgrade -y

3️⃣ Install Required Tools
A. Git
sudo apt install git -y

B. Build Tools
sudo apt install build-essential -y

4️⃣ Install Python, Pip, and Venv
sudo apt install python3 python3-pip python3-venv -y


(You may create virtual environments later if needed.)

5️⃣ Install Node.js (Needed for Gemini CLI, Claude CLI, MCP Tools)
Install Node.js LTS (20.x or 22.x)
curl -fsSL https://deb.nodesource.com/setup_22.x | sudo -E bash -
sudo apt install -y nodejs


Check versions:

node -v
npm -v

6️⃣ Fix npm Global Permissions (IMPORTANT)
Step 1 — Create global npm directory
mkdir ~/.npm-global

Step 2 — Point npm to use it
npm config set prefix ~/.npm-global

Step 3 — Update PATH
echo 'export PATH="$HOME/.npm-global/bin:$PATH"' >> ~/.bashrc
source ~/.bashrc

Step 4 — Install PNPM (no sudo needed)
npm install -g pnpm

7️⃣ Install the Gemini CLI
npm install -g @google/gemini-cli


Login:

gemini login


Initialize:

gemini init

8️⃣ Install Claude CLI
npm install -g claude-code


Login:

claude login

9️⃣ Install OpenAI CLI (optional but recommended)
npm install -g openai

🔟 Install Useful Utilities
Curl & Wget
sudo apt install curl wget -y

Unzip
sudo apt install unzip -y

jq (JSON tool, helpful for API debugging)
sudo apt install jq -y

1️⃣1️⃣ (Optional) Install VS Code in Ubuntu
sudo snap install code --classic

1️⃣2️⃣ Improve Your Bash Experience
nano ~/.bashrc


Add these:

alias ll='ls -lah'
alias g='git'
alias venv="python3 -m venv venv"


Apply:

source ~/.bashrc

✅ DONE — Environment Ready

You now have:

✔ Ubuntu WSL
✔ Node.js + npm + pnpm
✔ Python + pip + venv
✔ Gemini CLI
✔ Claude CLI
✔ OpenAI CLI
✔ Context7-ready environment
✔ Developer utilities
✔ Optional VS Code setup

To open this environment anytime:

Search WSL or Ubuntu in the Windows Start Menu.