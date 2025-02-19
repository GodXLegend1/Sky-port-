#!/bin/bash

# ASCII Art
ascii_art="
       ____           ___  ___                              _
 / ___| ___   __| \ \/ / |    ___  __ _  ___ _ __   __| |
| |  _ / _ \ / _` |\  /| |   / _ \/ _` |/ _ \ '_ \ / _` |
| |_| | (_) | (_| |/  \| |__|  __/ (_| |  __/ | | | (_| |
 \____|\___/ \__,_/_/\_\_____\___|\__, |\___|_| |_|\__,_|
                                  |___/
                                 
"

# Colors
RED='\033[0;31m'
GREEN='\033[0;32m'
BLUE='\033[0;34m'
CYAN='\033[0;36m'
YELLOW='\033[0;33m'
NC='\033[0m' # No Color

# Function to print messages
echo_message() {
  echo -e "${GREEN}$1${NC}"
}

# Clear the screen
clear

# Check if the script is run as root
if [ "$EUID" -ne 0 ]; then
  echo -e "${RED}Please run this script as root.${NC}"
  exit 1
fi

echo -e "${CYAN}$ascii_art${NC}"

echo_message "* Installing Dependencies"

# Update package list and install dependencies
sudo apt update
sudo apt install -y curl software-properties-common
curl -fsSL https://deb.nodesource.com/setup_20.x | sudo -E bash -
sudo apt-get install -y nodejs git

echo_message "* Installed Dependencies"

echo_message "* Installing Files"

# Create directory and clone repository
mkdir -p panel5
cd panel5 || { echo_message "Failed to change directory to panel5"; exit 1; }
git clone https://github.com/achul123/panel5.git panel_repo
cd panel_repo || { echo_message "Failed to change directory to panel_repo"; exit 1; }
npm install

echo_message "* Installed Files"

echo_message "* Starting Skyport"

# Run setup scripts
npm run seed
npm run createUser

echo_message "* Starting Skyport With PM2"

# Install PM2 and start the application
sudo npm install -g pm2
pm2 start index.js

echo_message "* Skyport Installed and Started on Port 3001"

# Clear the screen after finishing
clear
echo -e "${YELLOW}* Made by Jishnu${NC}"
