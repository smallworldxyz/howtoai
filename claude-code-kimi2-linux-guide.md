# Claude Code with Kimi2 API Setup Guide for Linux Users

A comprehensive guide for Linux developers to set up Claude Code with both Anthropic and Kimi2 (Moonshot) APIs, optimized for various Linux distributions and package managers.

## Table of Contents

1. [Prerequisites](#prerequisites)
2. [Step 1: Linux System Setup](#step-1-linux-system-setup)
3. [Step 2: Distribution-Specific Installation](#step-2-distribution-specific-installation)
4. [Step 3: Anthropic Account Setup](#step-3-anthropic-account-setup)
5. [Step 4: Kimi2 (Moonshot) Account Setup](#step-4-kimi2-moonshot-account-setup)
6. [Step 5: Installing Claude Code](#step-5-installing-claude-code)
7. [Step 6: Environment Configuration](#step-6-environment-configuration)
8. [Step 7: Advanced Linux Configuration](#step-7-advanced-linux-configuration)
9. [Step 8: Essential Commands and Usage](#step-8-essential-commands-and-usage)
10. [Step 9: System Integration](#step-9-system-integration)
11. [Step 10: Best Practices and Optimization](#step-10-best-practices-and-optimization)
12. [Step 11: Sample Command Prompts](#step-11-sample-command-prompts)
13. [Troubleshooting](#troubleshooting)

## Prerequisites

- Linux distribution (Ubuntu 20.04+, Debian 11+, CentOS 8+, Fedora 35+, Arch Linux)
- sudo/root access
- Stable internet connection
- Terminal familiarity
- curl/wget for downloads

---

## Step 1: Linux System Setup

### 1.1 System Update and Essential Tools

#### Ubuntu/Debian
```bash
sudo apt update && sudo apt upgrade -y
sudo apt install curl wget git build-essential software-properties-common apt-transport-https ca-certificates gnupg lsb-release -y
```

#### CentOS/RHEL/Fedora
```bash
# CentOS/RHEL
sudo yum update -y
sudo yum groupinstall "Development Tools" -y
sudo yum install curl wget git -y

# Fedora
sudo dnf update -y
sudo dnf groupinstall "Development Tools" -y
sudo dnf install curl wget git -y
```

#### Arch Linux
```bash
sudo pacman -Syu
sudo pacman -S base-devel curl wget git --noconfirm
```

#### openSUSE
```bash
sudo zypper refresh && sudo zypper update
sudo zypper install -t pattern devel_basis
sudo zypper install curl wget git
```

### 1.2 Install Node.js via Package Managers

#### Ubuntu/Debian (NodeSource)
```bash
curl -fsSL https://deb.nodesource.com/setup_20.x | sudo -E bash -
sudo apt-get install -y nodejs
```

#### CentOS/RHEL (NodeSource)
```bash
curl -fsSL https://rpm.nodesource.com/setup_20.x | sudo bash -
sudo yum install -y nodejs
```

#### Fedora (NodeSource)
```bash
curl -fsSL https://rpm.nodesource.com/setup_20.x | sudo bash -
sudo dnf install -y nodejs
```

#### Arch Linux (Official Repositories)
```bash
sudo pacman -S nodejs npm --noconfirm
```

#### openSUSE
```bash
sudo zypper install nodejs npm
```

#### Snap Package (Universal)
```bash
sudo snap install node --classic --channel=20
```

#### Verify Installation
```bash
node --version
npm --version
```

---

## Step 2: Distribution-Specific Installation

### 2.1 Ubuntu/Debian-based Systems

#### Using APT Package Manager
```bash
# Add Node.js repository (if not using NodeSource)
sudo apt update
sudo apt install nodejs npm -y

# Install Claude Code globally
sudo npm install -g @anthropic-ai/claude-code
```

#### Using Snap
```bash
# Install Node.js via snap
sudo snap install node --classic

# Install Claude Code
sudo npm install -g @anthropic-ai/claude-code
```

### 2.2 Red Hat-based Systems (RHEL/CentOS/Fedora)

#### Using DNF/YUM
```bash
# Enable EPEL repository (CentOS/RHEL)
sudo yum install epel-release -y

# Install Node.js and npm
sudo yum install nodejs npm -y  # CentOS/RHEL
sudo dnf install nodejs npm -y  # Fedora

# Install Claude Code
sudo npm install -g @anthropic-ai/claude-code
```

#### Using Node Version Manager (NVM)
```bash
# Install NVM
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.39.0/install.sh | bash
source ~/.bashrc

# Install Node.js LTS
nvm install --lts
nvm use --lts

# Install Claude Code globally
npm install -g @anthropic-ai/claude-code
```

### 2.3 Arch Linux

#### Using pacman
```bash
# Install from official repositories
sudo pacman -S nodejs npm --noconfirm

# Install Claude Code
sudo npm install -g @anthropic-ai/claude-code
```

#### Using AUR Helper (yay)
```bash
# Install yay if not available
sudo pacman -S --needed git base-devel

git clone https://aur.archlinux.org/yay.git
cd yay
makepkg -si

# Install Claude Code via AUR
yay -S claude-code-bin
```

### 2.4 openSUSE

#### Using zypper
```bash
# Install Node.js
sudo zypper install nodejs npm

# Install Claude Code
sudo npm install -g @anthropic-ai/claude-code
```

---

## Step 3: Anthropic Account Setup

### 3.1 Create Account

1. Visit [https://console.anthropic.com](https://console.anthropic.com)
2. Sign up with email or Google/GitHub account
3. Verify email address
4. Complete phone verification if required

### 3.2 Generate API Key

1. Go to [API Keys](https://console.anthropic.com/settings/keys)
2. Click "Create Key"
3. Name: "Linux Claude Code Development"
4. Copy the key immediately

### 3.3 Configure Environment

Add to shell profile based on your shell:

#### Bash (Ubuntu/Debian)
```bash
echo 'export ANTHROPIC_API_KEY="your-anthropic-key-here"' >> ~/.bashrc
source ~/.bashrc
```

#### Zsh (macOS, some Linux distros)
```bash
echo 'export ANTHROPIC_API_KEY="your-anthropic-key-here"' >> ~/.zshrc
source ~/.zshrc
```

#### Fish shell
```bash
set -Ux ANTHROPIC_API_KEY "your-anthropic-key-here"
```

#### System-wide (all users)
```bash
echo 'ANTHROPIC_API_KEY="your-anthropic-key-here"' | sudo tee /etc/environment
```

---

## Step 4: Kimi2 (Moonshot) Account Setup

### 4.1 Create Moonshot Account

1. Visit [https://platform.moonshot.cn](https://platform.moonshot.cn)
2. Click "注册" (Sign Up)
3. Register with email or phone
4. Complete verification
5. Log in to console

### 4.2 Generate API Key

1. Navigate to [API Keys管理](https://platform.moonshot.cn/console/api-keys)
2. Click "创建 API Key"
3. Name: "Linux Kimi2 Development"
4. Select permissions: "全部权限"
5. Copy key immediately

### 4.3 Configure Environment

```bash
# Add to shell profile
echo 'export KIMI2_API_KEY="your-kimi2-key-here"' >> ~/.bashrc
source ~/.bashrc
```

---

## Step 5: Installing Claude Code

### 5.1 Global Installation

```bash
# Using npm
sudo npm install -g @anthropic-ai/claude-code

# Or using yarn
sudo yarn global add @anthropic-ai/claude-code

# Or using pnpm
sudo pnpm add -g @anthropic-ai/claude-code
```

### 5.2 Verify Installation

```bash
claude --version
which claude
```

### 5.3 Alternative Installation Methods

#### User-local Installation (no sudo)
```bash
mkdir -p ~/.local/bin
npm install @anthropic-ai/claude-code --prefix ~/.local
echo 'export PATH="$HOME/.local/bin:$PATH"' >> ~/.bashrc
source ~/.bashrc
```

#### Docker Installation
```bash
# Create Dockerfile
cat > Dockerfile << EOF
FROM node:20-alpine
RUN npm install -g @anthropic-ai/claude-code
WORKDIR /workspace
ENTRYPOINT ["claude"]
EOF

# Build and run
docker build -t claude-code .
docker run -it -v $(pwd):/workspace claude-code
```

---

## Step 6: Environment Configuration

### 6.1 Create Configuration Directory

```bash
mkdir -p ~/.config/claude-code
mkdir -p ~/.local/share/claude-code
```

### 6.2 Provider Configuration Files

#### Anthropic Configuration
Create `~/.config/claude-code/anthropic.json`:

```json
{
  "provider": "anthropic",
  "apiKey": "${ANTHROPIC_API_KEY}",
  "model": "claude-3-5-sonnet-20241022",
  "maxTokens": 4000,
  "temperature": 0.7,
  "baseURL": "https://api.anthropic.com"
}
```

#### Kimi2 Configuration
Create `~/.config/claude-code/kimi2.json`:

```json
{
  "provider": "moonshot",
  "apiKey": "${KIMI2_API_KEY}",
  "model": "kimi",
  "maxTokens": 4000,
  "temperature": 0.7,
  "baseURL": "https://api.moonshot.cn/v1"
}
```

### 6.3 Create Switching Script

Create `~/.local/bin/claude-switch`:

```bash
#!/bin/bash

PROVIDER="${1:-anthropic}"
CONFIG_DIR="$HOME/.config/claude-code"
CURRENT_CONFIG="$CONFIG_DIR/config.json"

if [[ "$PROVIDER" == "anthropic" ]]; then
    cp "$CONFIG_DIR/anthropic.json" "$CURRENT_CONFIG"
    echo "✓ Switched to Anthropic (Claude 3.5 Sonnet)"
elif [[ "$PROVIDER" == "kimi2" ]]; then
    cp "$CONFIG_DIR/kimi2.json" "$CURRENT_CONFIG"
    echo "✓ Switched to Kimi2 (Moonshot)"
elif [[ "$PROVIDER" == "status" ]]; then
    if [[ -f "$CURRENT_CONFIG" ]]; then
        CURRENT=$(jq -r '.provider' "$CURRENT_CONFIG" 2>/dev/null || echo "unknown")
        echo "Current provider: $CURRENT"
    else
        echo "No active configuration"
    fi
else
    echo "Usage: claude-switch [anthropic|kimi2|status]"
    exit 1
fi
```

Make it executable:
```bash
chmod +x ~/.local/bin/claude-switch
```

### 6.4 Shell Integration

Add to your shell profile for auto-completion:

```bash
# Add to ~/.bashrc or ~/.zshrc
complete -W "anthropic kimi2 status" claude-switch

# Create alias
alias cs='claude-switch'
```

---

## Step 7: Advanced Linux Configuration

### 7.1 Systemd Service (Optional)

Create systemd user service for Claude Code daemon:

```bash
# Create systemd user directory
mkdir -p ~/.config/systemd/user

# Create service file
cat > ~/.config/systemd/user/claude-code.service << EOF
[Unit]
Description=Claude Code Daemon
After=graphical-session.target

[Service]
Type=simple
ExecStart=%h/.local/bin/claude --daemon
Restart=on-failure
RestartSec=10
Environment=ANTHROPIC_API_KEY=%i
Environment=KIMI2_API_KEY=%i

[Install]
WantedBy=default.target
EOF

# Enable and start service
systemctl --user daemon-reload
systemctl --user enable claude-code.service
systemctl --user start claude-code.service
```

### 7.2 Desktop Integration

#### Create Desktop Entry
```bash
# Create desktop file
cat > ~/.local/share/applications/claude-code.desktop << EOF
[Desktop Entry]
Type=Application
Name=Claude Code
Comment=AI-powered coding assistant
Exec=claude
Icon=utilities-terminal
Terminal=true
Categories=Development;IDE;
Keywords=ai;code;assistant;
EOF

# Update desktop database
update-desktop-database ~/.local/share/applications/
```

### 7.3 Shell Functions

Add convenient functions to your shell profile:

```bash
# Add to ~/.bashrc or ~/.zshrc

# Quick Claude starter
cl() {
    local dir="${1:-.}"
    cd "$dir" && claude /init
}

# Provider info
claude-info() {
    echo "=== Claude Code Information ==="
    echo "Version: $(claude --version 2>/dev/null || echo 'Not installed')"
    echo "Config Dir: $HOME/.config/claude-code"
    echo "Current Provider: $(claude-switch status 2>/dev/null || echo 'Unknown')"
    echo "API Keys:"
    echo "  ANTHROPIC_API_KEY: ${ANTHROPIC_API_KEY:+Set} ${ANTHROPIC_API_KEY:-Not set}"
    echo "  KIMI2_API_KEY: ${KIMI2_API_KEY:+Set} ${KIMI2_API_KEY:-Not set}"
}

# Environment checker
claude-check() {
    echo "Checking Claude Code setup..."
    
    # Check if claude is in PATH
    if command -v claude >/dev/null 2>&1; then
        echo "✓ Claude Code is installed"
    else
        echo "✗ Claude Code not found in PATH"
        return 1
    fi
    
    # Check API keys
    if [[ -n "$ANTHROPIC_API_KEY" ]]; then
        echo "✓ ANTHROPIC_API_KEY is set"
    else
        echo "✗ ANTHROPIC_API_KEY is not set"
    fi
    
    if [[ -n "$KIMI2_API_KEY" ]]; then
        echo "✓ KIMI2_API_KEY is set"
    else
        echo "✗ KIMI2_API_KEY is not set"
    fi
    
    # Check config files
    if [[ -f "$HOME/.config/claude-code/anthropic.json" ]]; then
        echo "✓ Anthropic config exists"
    else
        echo "✗ Anthropic config missing"
    fi
    
    if [[ -f "$HOME/.config/claude-code/kimi2.json" ]]; then
        echo "✓ Kimi2 config exists"
    else
        echo "✗ Kimi2 config missing"
    fi
}
```

---

## Step 8: Essential Commands and Usage

### 8.1 Basic Commands

| Command | Description | Example |
|---------|-------------|---------|
| `claude` | Start interactive mode | `claude` |
| `claude /init` | Initialize in current dir | `claude /init` |
| `claude /agents` | List available agents | `claude /agents` |
| `claude /status` | Check system status | `claude /status` |
| `claude --help` | Show help | `claude --help` |

### 8.2 Project Initialization

```bash
# Initialize new project
mkdir my-project && cd my-project
claude /init

# Initialize with specific provider
claude-switch kimi2 && claude /init
```

### 8.3 Working with Agents

```bash
# List all agents
claude /agents

# Use specific agent
claude --agent general-purpose "Explain this code"

# Custom agent example
claude --agent code-reviewer "Review this PR"
```

### 8.4 Advanced Usage

```bash
# Batch processing
find . -name "*.py" -exec claude "Review {}" \;

# Git integration
claude "Generate commit message for these changes"

# File analysis
claude "Find security issues in src/"
```

---

## Step 9: System Integration

### 9.1 Git Hooks Integration

Create pre-commit hook:

```bash
# Create git hook
mkdir -p .git/hooks
cat > .git/hooks/pre-commit << 'EOF'
#!/bin/bash
# Claude Code pre-commit hook

if command -v claude >/dev/null 2>&1; then
    echo "Running Claude Code security check..."
    claude "Check for security issues in staged files" --brief
fi
EOF

chmod +x .git/hooks/pre-commit
```

### 9.2 IDE Integration

#### VS Code Integration
```bash
# Install via VS Code marketplace
# Extension: "Claude Code"
```

#### Vim/Neovim Integration
```bash
# Using vim-plug
# Add to ~/.vimrc or ~/.config/nvim/init.vim
# Plug 'claude-code/vim-claude'
```

### 9.3 Docker Integration

Create `Dockerfile.claude`:

```dockerfile
FROM node:20-alpine

# Install Claude Code
RUN npm install -g @anthropic-ai/claude-code

# Set working directory
WORKDIR /workspace

# Copy configuration
COPY .claude/ /root/.config/claude-code/

# Set environment variables
ENV ANTHROPIC_API_KEY=""
ENV KIMI2_API_KEY=""

# Default command
CMD ["claude"]
```

Build and run:
```bash
docker build -f Dockerfile.claude -t claude-dev .
docker run -it -v $(pwd):/workspace -e ANTHROPIC_API_KEY=$ANTHROPIC_API_KEY claude-dev
```

---

## Step 10: Best Practices and Optimization

### 10.1 Performance Optimization

#### Node.js Optimization
```bash
# Increase memory limit
export NODE_OPTIONS="--max-old-space-size=4096"

# Enable performance mode
echo 'export NODE_ENV=production' >> ~/.bashrc
```

#### Network Optimization
```bash
# Configure proxy if needed
export HTTP_PROXY="http://proxy.company.com:8080"
export HTTPS_PROXY="http://proxy.company.com:8080"
```

### 10.2 Security Best Practices

#### File Permissions
```bash
# Secure config directory
chmod 700 ~/.config/claude-code
chmod 600 ~/.config/claude-code/*.json

# Secure API keys
chmod 600 ~/.bashrc
chmod 600 ~/.zshrc
```

#### SSH Integration
```bash
# Add to SSH config for secure connections
# ~/.ssh/config
Host github.com
    StrictHostKeyChecking yes
    UserKnownHostsFile ~/.ssh/known_hosts
```

### 10.3 Backup Configuration

```bash
# Backup script
cat > ~/.local/bin/backup-claude-config << 'EOF'
#!/bin/bash
BACKUP_DIR="$HOME/.local/share/claude-backups"
mkdir -p "$BACKUP_DIR"
tar -czf "$BACKUP_DIR/claude-config-$(date +%Y%m%d-%H%M%S).tar.gz" \
    ~/.config/claude-code \
    ~/.claude
EOF

chmod +x ~/.local/bin/backup-claude-config
```

---

## Step 11: Sample Command Prompts

### 11.1 Development Workflows

#### Code Analysis
```bash
# Switch to Claude for complex analysis
claude-switch anthropic
claude "Analyze this codebase for architectural patterns and suggest improvements"

# Switch to Kimi2 for performance analysis
claude-switch kimi2
claude "Profile this Python script and identify bottlenecks"
```

#### Security Review
```bash
# Security scan with Claude
claude-switch anthropic
claude "Perform security audit on this web application"

# Dependency check with Kimi2
claude-switch kimi2
claude "Check package.json for known vulnerabilities"
```

#### Documentation Generation
```bash
# Technical docs with Claude
claude-switch anthropic
claude "Generate API documentation from code comments"

# Multi-language docs with Kimi2
claude-switch kimi2
claude "Create README in English and Chinese"
```

### 11.2 System Administration

#### Server Configuration
```bash
# Analyze nginx config
claude "Review this nginx configuration for security and performance"

# Docker optimization
claude "Optimize this Dockerfile for production"
```

#### Log Analysis
```bash
# Parse system logs
claude "Analyze /var/log/syslog for errors in the last hour"

# Performance monitoring
claude "Create monitoring script for disk usage alerts"
```

### 11.3 Advanced Patterns

#### Batch Processing
```bash
# Process multiple repositories
for repo in */; do
    (cd "$repo" && claude "Generate summary for this project")
done
```

#### Integration Scripts
```bash
# CI/CD integration
claude "Create GitHub Actions workflow for automated testing"

# Database migration
claude "Generate SQL migration script for schema changes"
```

---

## Troubleshooting

### Common Issues and Solutions

#### 1. Permission Denied Errors

**Symptoms**: `EACCES: permission denied`

**Solutions**:
```bash
# Fix npm permissions
sudo chown -R $(whoami) ~/.npm

# Fix global installation
sudo chown -R $(whoami) $(npm config get prefix)/{lib/node_modules,bin,share}
```

#### 2. Node.js Version Issues

**Symptoms**: `Error: Node.js version incompatible`

**Solutions**:
```bash
# Check Node.js version
node --version

# Update Node.js (Ubuntu/Debian)
curl -fsSL https://deb.nodesource.com/setup_20.x | sudo -E bash -
sudo apt-get install -y nodejs

# Or use nvm
nvm install 20
nvm use 20
```

#### 3. API Connection Issues

**Symptoms**: `Network timeout`, `Connection refused`

**Solutions**:
```bash
# Test API connectivity
curl -I https://api.anthropic.com
curl -I https://api.moonshot.cn

# Check firewall
sudo ufw status
sudo iptables -L

# Check DNS
nslookup api.anthropic.com
nslookup api.moonshot.cn
```

#### 4. Configuration Issues

**Symptoms**: `Config file not found`, `Invalid API key`

**Solutions**:
```bash
# Verify configuration
claude-check

# Reset configuration
rm -rf ~/.config/claude-code/config.json
claude-switch anthropic

# Check environment variables
echo $ANTHROPIC_API_KEY | wc -c  # Should be > 0
echo $KIMI2_API_KEY | wc -c      # Should be > 0
```

#### 5. Memory Issues

**Symptoms**: `JavaScript heap out of memory`

**Solutions**:
```bash
# Increase Node.js memory limit
export NODE_OPTIONS="--max-old-space-size=8192"

# Monitor memory usage
htop
free -h
```

#### 6. SSL Certificate Issues

**Symptoms**: `SSL certificate verify failed`

**Solutions**:
```bash
# Update CA certificates
sudo apt update ca-certificates  # Ubuntu/Debian
sudo yum update ca-certificates  # CentOS/RHEL
sudo dnf update ca-certificates  # Fedora

# Check system time
date
sudo ntpdate -s time.nist.gov
```

### Debug Mode

Enable detailed logging:
```bash
export CLAUDE_DEBUG=1
export NODE_DEBUG=net,http,https
claude
```

### Getting Help

1. **Claude Code Documentation**: [https://docs.anthropic.com/en/docs/claude-code](https://docs.anthropic.com/en/docs/claude-code)
2. **Moonshot Documentation**: [https://platform.moonshot.cn/docs](https://platform.moonshot.cn/docs)
3. **System Logs**: `journalctl --user -u claude-code`
4. **Community**: GitHub Issues, Reddit r/linux, Stack Overflow

---

## Quick Reference Card

```bash
# Installation commands by distribution

# Ubuntu/Debian
sudo apt update && sudo apt install nodejs npm -y
sudo npm install -g @anthropic-ai/claude-code

# CentOS/RHEL
sudo yum install epel-release -y
sudo yum install nodejs npm -y
sudo npm install -g @anthropic-ai/claude-code

# Fedora
sudo dnf install nodejs npm -y
sudo npm install -g @anthropic-ai/claude-code

# Arch Linux
sudo pacman -S nodejs npm --noconfirm
sudo npm install -g @anthropic-ai/claude-code

# Configuration
claude-check           # Check setup
claude-switch anthropic # Switch to Claude
claude-switch kimi2     # Switch to Kimi2
claude-info            # Show system info

# Daily usage
claude                 # Start interactive mode
claude /init           # Initialize project
claude /agents         # List agents
claude /status         # Check status
```

---

*This guide is optimized for Linux distributions by smallworld and the community. Last updated: 2025-08-12*
