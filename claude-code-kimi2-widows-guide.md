# Claude Code with Kimi2 API Setup Guide for Windows Users

A comprehensive guide for Windows developers to set up Claude Code with both Anthropic and Kimi2 (Moonshot) APIs, allowing seamless switching between models.

## Table of Contents

1. [Prerequisites](#prerequisites)
2. [Step 1: Setting up Ubuntu WSL](#step-1-setting-up-ubuntu-wsl)
3. [Step 2: Anthropic Account Setup](#step-2-anthropic-account-setup)
4. [Step 3: Kimi2 (Moonshot) Account Setup](#step-3-kimi2-moonshot-account-setup)
5. [Step 4: Installing Claude Code](#step-4-installing-claude-code)
6. [Step 5: Configuring API Switching](#step-5-configuring-api-switching)
7. [Step 6: Essential Commands and Usage](#step-6-essential-commands-and-usage)
8. [Step 7: Best Practices](#step-7-best-practices)
9. [Step 8: Sample Command Prompts](#step-8-sample-command-prompts)
10. [Troubleshooting](#troubleshooting)

## Prerequisites

- Windows 10 version 2004 and higher (Build 19041 and higher) or Windows 11
- Administrator access on your Windows machine
- Stable internet connection
- Basic familiarity with command line interfaces

---

## Step 1: Setting up Ubuntu WSL

### 1.1 Enable WSL and Install Ubuntu

Open PowerShell as Administrator and run:

```powershell
wsl --install -d Ubuntu
```

If WSL is already installed, update it:

```powershell
wsl --update
```

### 1.2 Initial Ubuntu Setup

After installation, launch Ubuntu from the Start menu. You'll be prompted to create a username and password.

### 1.3 Update Ubuntu Packages

```bash
sudo apt update && sudo apt upgrade -y
```

### 1.4 Install Essential Tools

```bash
sudo apt install curl wget git build-essential -y
```

### 1.5 Install Node.js and npm

```bash
curl -fsSL https://deb.nodesource.com/setup_20.x | sudo -E bash -
sudo apt-get install -y nodejs
```

Verify installation:

```bash
node --version
npm --version
```

---

## Step 2: Anthropic Account Setup

### 2.1 Create Anthropic Account

1. Visit [https://console.anthropic.com](https://console.anthropic.com)
2. Click "Sign Up" and complete registration
3. Verify your email address
4. Log in to your account

### 2.2 Generate API Key

1. Navigate to [API Keys section](https://console.anthropic.com/settings/keys)
2. Click "Create Key"
3. Give your key a descriptive name (e.g., "Claude Code Development")
4. Copy the API key immediately (it won't be shown again)
5. Store it securely in a password manager

### 2.3 Set Environment Variable

In your Ubuntu terminal, add the API key to your shell profile:

```bash
echo 'export ANTHROPIC_API_KEY="your-anthropic-api-key-here"' >> ~/.bashrc
source ~/.bashrc
```

---

## Step 3: Kimi2 (Moonshot) Account Setup

### 3.1 Create Moonshot Account

1. Visit [https://platform.moonshot.cn](https://platform.moonshot.cn)
2. Click "注册" (Sign Up) in the top right
3. Complete registration with email/phone
4. Verify your account through email/SMS
5. Log in to your account

### 3.2 Generate Kimi2 API Key

1. Navigate to [API Keys管理](https://platform.moonshot.cn/console/api-keys)
2. Click "创建 API Key" (Create API Key)
3. Enter a name for your key (e.g., "Claude Code Kimi2")
4. Select appropriate permissions (typically "全部权限" for development)
5. Copy the API key immediately

### 3.3 Set Environment Variable

In your Ubuntu terminal, add the Kimi2 API key:

```bash
echo 'export KIMI2_API_KEY="your-kimi2-api-key-here"' >> ~/.bashrc
source ~/.bashrc
```

---

## Step 4: Installing Claude Code

### 4.1 Install Claude Code Globally

```bash
npm install -g @anthropic-ai/claude-code
```

### 4.2 Verify Installation

```bash
claude --version
```

### 4.3 Initial Setup

Run Claude Code for the first time:

```bash
claude
```

Follow the interactive setup prompts:
1. Accept the terms of service
2. Configure your preferred settings
3. Test the connection to Anthropic API

---

## Step 5: Configuring API Switching

### 5.1 Create Configuration Files

Create a configuration directory:

```bash
mkdir -p ~/.claude-code
```

### 5.2 Anthropic Configuration

Create `~/.claude-code/anthropic-config.json`:

```json
{
  "provider": "anthropic",
  "apiKey": "${ANTHROPIC_API_KEY}",
  "model": "claude-3-5-sonnet-20241022",
  "maxTokens": 4000,
  "temperature": 0.7
}
```

### 5.3 Kimi2 Configuration

Create `~/.claude-code/kimi2-config.json`:

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

### 5.4 Create Switching Script

Create `~/.claude-code/switch-provider.sh`:

```bash
#!/bin/bash

PROVIDER=$1

if [ "$PROVIDER" = "anthropic" ]; then
    cp ~/.claude-code/anthropic-config.json ~/.claude-code/config.json
    echo "Switched to Anthropic (Claude)"
elif [ "$PROVIDER" = "kimi2" ]; then
    cp ~/.claude-code/kimi2-config.json ~/.claude-code/config.json
    echo "Switched to Kimi2 (Moonshot)"
else
    echo "Usage: switch-provider.sh [anthropic|kimi2]"
    exit 1
fi
```

Make it executable:

```bash
chmod +x ~/.claude-code/switch-provider.sh
```

Add alias to ~/.bashrc:

```bash
echo 'alias claude-switch="~/.claude-code/switch-provider.sh"' >> ~/.bashrc
source ~/.bashrc
```

---

## Step 6: Essential Commands and Usage

### 6.1 Basic Commands

| Command | Description |
|---------|-------------|
| `claude` | Start Claude Code interactive mode |
| `claude --help` | Show all available commands |
| `claude /init` | Initialize Claude Code in current directory |
| `claude /agents` | List available agents |
| `claude /status` | Check current configuration and API status |

### 6.2 Working with Agents

#### List Available Agents

```bash
claude /agents
```

#### Use Specific Agent

```bash
claude --agent general-purpose
```

#### Custom Agent Creation

Create `.claude/agents/custom-agent.json`:

```json
{
  "name": "custom-agent",
  "description": "Custom agent for specific tasks",
  "tools": ["Read", "Write", "Edit", "Bash"],
  "prompt": "You are a specialized agent for..."
}
```

### 6.3 Project Initialization

#### Initialize New Project

```bash
mkdir my-project && cd my-project
claude /init
```

#### Configure Project Settings

Create `.claude/config.json` in project root:

```json
{
  "provider": "anthropic",
  "model": "claude-3-5-sonnet-20241022",
  "excludePatterns": ["node_modules/**", "*.log", ".git/**"],
  "maxContextLength": 100000
}
```

---

## Step 7: Best Practices

### 7.1 API Key Security

1. **Never commit API keys to version control**
   - Add `.claude/` to `.gitignore`
   - Use environment variables for sensitive data

2. **Rotate keys regularly**
   - Set calendar reminders every 90 days
   - Update both Anthropic and Kimi2 keys

3. **Use different keys for different environments**
   - Development: Personal keys
   - Production: Service account keys

### 7.2 Model Selection Guidelines

| Use Case | Recommended Model |
|----------|-------------------|
| Code Review | Claude 3.5 Sonnet |
| Complex Analysis | Kimi2 |
| Creative Tasks | Claude 3.5 Sonnet |
| Chinese Content | Kimi2 |
| Performance Critical | Kimi2 |

### 7.3 Context Management

1. **Keep context focused**
   - Use `.claudeignore` for large directories
   - Split large files into smaller chunks

2. **Regular cleanup**
   - Clear conversation history with `/clear`
   - Restart sessions for fresh context

### 7.4 Performance Optimization

1. **Network considerations**
   - Anthropic: Global CDN, good worldwide
   - Kimi2: Optimized for China, use VPN if needed

2. **Rate limiting**
   - Respect API rate limits
   - Implement exponential backoff

---

## Step 8: Sample Command Prompts

### 8.1 Development Workflows

#### Code Review
```bash
# Switch to Claude for code review
claude-switch anthropic
claude "Review this pull request for security issues and code quality"

# Switch to Kimi2 for performance analysis
claude-switch kimi2
claude "Analyze this algorithm's time complexity and suggest optimizations"
```

#### Debugging
```bash
# Use Claude for complex debugging
claude-switch anthropic
claude "I'm getting a null pointer exception in line 42, help me trace the issue"

# Use Kimi2 for stack trace analysis
claude-switch kimi2
claude "Explain this error message and suggest fixes: [paste error]"
```

#### Documentation
```bash
# Claude for technical documentation
claude-switch anthropic
claude "Generate comprehensive API documentation for this module"

# Kimi2 for multilingual docs
claude-switch kimi2
claude "Create README.md in both English and Chinese"
```

### 8.2 Advanced Usage Patterns

#### Batch Processing
```bash
# Process multiple files
claude "Analyze all .js files in src/ directory for security vulnerabilities"

# Generate reports
claude "Create a summary report of all TODO comments in the codebase"
```

#### Integration with Git
```bash
# Pre-commit hooks
claude "Check if these changes might break existing functionality"

# PR descriptions
claude "Generate a detailed PR description for these changes"
```

#### Testing Workflows
```bash
# Generate test cases
claude "Create unit tests for this function with edge cases"

# Test coverage analysis
claude "Identify areas with poor test coverage in this module"
```

---

## Troubleshooting

### Common Issues

#### 1. Connection Timeouts

**Symptoms**: API calls hanging or timing out
**Solutions**:
- Check internet connection
- Verify API key validity
- Try switching providers
- Check rate limits

#### 2. Permission Errors

**Symptoms**: "Permission denied" when running scripts
**Solutions**:
```bash
chmod +x ~/.claude-code/switch-provider.sh
```

#### 3. Model Not Found

**Symptoms**: "Model not available" errors
**Solutions**:
- Update model names in config files
- Check API provider documentation
- Verify subscription tier supports model

#### 4. WSL Issues

**Symptoms**: Commands not found in WSL
**Solutions**:
```bash
# Refresh environment
source ~/.bashrc

# Check PATH
echo $PATH

# Reinstall if needed
npm install -g @anthropic-ai/claude-code
```

### Getting Help

1. **Claude Code Documentation**: [https://docs.anthropic.com/en/docs/claude-code](https://docs.anthropic.com/en/docs/claude-code)
2. **Moonshot Documentation**: [https://platform.moonshot.cn/docs](https://platform.moonshot.cn/docs)
3. **Community Support**: GitHub Issues, Stack Overflow

### Debug Mode

Enable debug logging:

```bash
export CLAUDE_DEBUG=1
claude
```

---

## Quick Reference Card

```bash
# Setup commands
wsl --install -d Ubuntu
npm install -g @anthropic-ai/claude-code

# Configuration
claude-switch anthropic  # Switch to Claude
claude-switch kimi2      # Switch to Kimi2

# Daily usage
claude                   # Start interactive mode
claude /init             # Initialize project
claude /agents           # List agents
claude /status           # Check status

# Environment variables
echo $ANTHROPIC_API_KEY
echo $KIMI2_API_KEY
```

---

*This guide is maintained by smallworld and the community. Last updated: 2025-08-12*