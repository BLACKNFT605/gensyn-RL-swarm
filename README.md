# gensyn-RL-swarm
Easy guide to run Gensyn RL-Swarm node.

# ⭐ RL Swarm Testnet Node — Clean, Human-Written Setup Guide

RL Swarm is an open-source framework created by GensynAI that lets you run distributed reinforcement-learning workers over the internet.
This guide walks you through setting up an RL Swarm node, enabling the dashboard, installing Ngrok, fixing common errors, and configuring the Telegram monitoring bot.

## 🔧 Hardware Requirements
### CPU-Only

Minimum 16 GB RAM
(Recommended to use more for larger models or workloads)

### Optional GPU Support

Supports CUDA GPUs:

RTX 3090

RTX 4090

A100

H100

You can run the node with CPU only if you don’t have a GPU.

# 🚀 RL Swarm Node Setup (Ubuntu)
## 1. Create a backup directory
mkdir swarm.backup

### 2. Copy your swarm.pem file
cp rl-swarm/swarm.pem swarm.backup

### 3. Delete the old rl-swarm folder
rm -rf rl-swarm

### 4. Install Python & Yarn
sudo apt update && sudo apt install -y python3 python3-venv python3-pip curl wget screen git lsof && curl -sS https://dl.yarnpkg.com/debian/pubkey.gpg | sudo apt-key add - && echo "deb https://dl.yarnpkg.com/debian/ stable main" | sudo tee /etc/apt/sources.list.d/yarn.list && sudo apt update && sudo apt install -y yarn

### 5. Install Node.js
curl -fsSL https://deb.nodesource.com/setup_22.x | sudo -E bash -
sudo apt install -y nodejs

### 6. Remove old Python venv
rm -rf .venv


### Create & activate a new one:

python3 -m venv .venv
source .venv/bin/activate

### 7. Clone the Swarm repository
git clone https://github.com/gensyn-ai/rl-swarm.git
cd rl-swarm

### 8. Run RL Swarm
### CPU-only:
CPU_ONLY=true ./run_rl_swarm.sh

### GPU:
./run_rl_swarm.sh

## 🌐 Ngrok Setup (for Web Dashboard)

### Open a new Ubuntu window.

### 9. Install Ngrok
wget https://bin.equinox.io/c/bNyj1mQVY4c/ngrok-v3-stable-linux-amd64.tgz && tar -xvzf ngrok-v3-stable-linux-amd64.tgz && sudo mv ngrok /usr/local/bin/


Go to: https://ngrok.com

Sign up

Open Authtoken page

Copy your token

Paste and run it in terminal

### 10. Start Ngrok
ngrok http 3000

### 11. Copy your .free link

Open it in Chrome and follow the setup.

🔄 Restore swarm.pem and run again
### 12. Copy the backup swarm.pem
cp swarm.backup/swarm.pem rl-swarm

### 13. Activate Python
python3 -m venv .venv
source .venv/bin/activate

### 14. Clone RL Swarm again
git clone https://github.com/gensyn-ai/rl-swarm.git
cd rl-swarm

### 15. Run the node again

CPU:

CPU_ONLY=true ./run_rl_swarm.sh


GPU:

./run_rl_swarm.sh

### 16. When asked about AI prediction model

### Press:

Y

# ❗ Fixing the “New Error Coming On Gensyn Node”

If you get the error shown in your screenshot, reset your repository.

### 1. Activate venv
python3 -m venv .venv
source .venv/bin/activate

### 2. Enter rl-swarm folder
cd rl-swarm

### 3. Reset & update
git switch main
git reset --hard
git clean -fd
git pull origin main

### 4. Run the node
./run_rl_swarm.sh

# 🤖 Gswarm Role — Telegram Bot Setup

This is required for earning The Swarm Discord role.

### 🟦 Step 1 — Install Gswarm
Install Go:
sudo rm -rf /usr/local/go
curl -L https://go.dev/dl/go1.22.4.linux-amd64.tar.gz | sudo tar -xzf - -C /usr/local
echo 'export PATH=$PATH:/usr/local/go/bin:$HOME/go/bin' >> $HOME/.bash_profile
echo 'export PATH=$PATH:$(go env GOPATH)/bin' >> $HOME/.bash_profile
source .bash_profile
go version

### Install gswarm:
go install github.com/Deep-Commit/gswarm/cmd/gswarm@latest

### Verify:
gswarm --version

## 🟦 Step 2 — Create Telegram Bot

Open @BotFather

Send /newbot

Save the bot token

Get your chat ID

Send any message to your new bot, then open:

https://api.telegram.org/botYOUR_BOT_TOKEN/getUpdates


Find "chat":{"id":123456789} → that number is your chat ID.

### 🟦 Step 3 — Run the Gswarm bot

Run:

gswarm


Enter:

Bot token

Chat ID

Your EOA address (found in Gensyn dashboard)

### 🟦 Step 4 — Link Discord and Telegram

Open Discord → go to #|swarm-link

Run:

/link-telegram


You will receive a code.

In your Telegram bot:

/verify <code>


This links your accounts and unlocks The Swarm role.

# 🛟 Backup Your swarm.pem

## Highly recommended — run this script:

[ -f backup.sh ] && rm backup.sh; curl -sSL -O https://raw.githubusercontent.com/zunxbt/gensyn-test
