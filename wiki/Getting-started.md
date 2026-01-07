# Getting started

This guide walks you through installing and using the Content Developer Assistant.

---

## Prerequisites

Before you begin, ensure you have:

- **Windows 10 or later** (or Mac/Linux for manual setup)
- **GitHub Copilot subscription** - Required for agent functionality
- **Microsoft account** - For Azure DevOps access
- **GitHub account** - For repository access

---

## Installation

### Option 1: Automated installation (recommended)

1. **Run the installer**:
   - Double-click `Content Developer Setup.exe`
   - Follow the installation wizard
   - The installer will:
     - Install all required tools (VS Code, Git, Node.js, Azure CLI, GitHub CLI)
     - Configure MCP servers
     - Download the latest agent file
     - Set up your user profile

2. **Restart VS Code**

### Option 2: Manual setup

See the [README.md](../README.md) for manual installation instructions.

---

## First-time setup

### Step 1: Sign into GitHub Copilot

**This is the most critical step!**

1. Open VS Code
2. Look for the GitHub Copilot icon in the **bottom-right status bar**
3. Click the icon and sign in with your GitHub account
4. **Without this, you won't see any @-agents in Copilot Chat**

### Step 2: Configure agent mode and model

1. **Select the model**: 
   - Click the model selector in Copilot Chat
   - Choose **Claude Sonnet 4.5** (recommended for best results)
   - Feel free to experiment with other models

2. **Activate agent mode**:
   - In Copilot Chat settings, select **content-developer** as your agent mode
   - This enables the specialized documentation workflow automation

### Step 3: Verify agent is available

1. Open GitHub Copilot Chat (Ctrl+Shift+I or Cmd+Shift+I on Mac)
2. Type `@` and verify you see `@content-developer-assistant`
3. If not visible, restart VS Code and check again

### Step 4: Complete environment setup

**IMPORTANT**: Before you can use ADO and GitHub MCP tools, you must authenticate.

Ask the agent to guide you through authentication:

```
@content-developer-assistant help me complete my environment setup
```

The agent will provide ready-to-copy commands for:

1. **Azure authentication**: `az login` - Connect to Azure DevOps
2. **GitHub authentication**: `gh auth login` - Connect to GitHub
3. **Git configuration**: Set up your name, email, and recommended settings
4. **Verification steps**: Confirm everything is working

**Run these commands in your terminal before proceeding to Step 5.**

### Step 5: Clone your repository

If you're working on Azure documentation, the agent can help you clone the correct repository:

**From a Learn article URL**:
```
@content-developer-assistant help me clone https://learn.microsoft.com/en-us/azure/expressroute/expressroute-introduction
```

**Or by repository name**:
```
@content-developer-assistant help me clone azure-docs-pr
```

The agent will:
- Determine the correct private repository (adds `-pr` suffix)
- Check if you have a fork
- Generate shallow clone commands (`--depth 5`) for faster cloning
- Set up upstream remote

---

## Your first workflow

Once setup is complete, try creating your first work item:

```
@content-developer-assistant I need to create a work item
```

The agent will guide you through:
1. Creating an ADO work item with auto-calculated fields
2. Making your documentation changes
3. Committing files with proper git workflow
4. Creating a PR with AB# linking
5. Updating and closing the work item

See [Common workflows](Common-workflows.md) for detailed examples.

---

## Verify installation

Test that everything is working:

```
@content-developer-assistant get_workflow_example workflow_type='all'
```

This should return a quick reference of all available workflows.

---

## Troubleshooting

### Agent not showing up?

**Most common issue**: Not signed into GitHub Copilot

- Check bottom-right status bar in VS Code (look for GitHub Copilot icon)
- Click and sign in with your GitHub account
- Restart VS Code after signing in
- Open Copilot Chat and type `@` to verify

### MCP servers not working?

- **Did you run the authentication commands?**
  - Run `az login` for Azure DevOps access
  - Run `gh auth login` for GitHub access
- Verify you're connected to the **MSFT-AzVPN-Manual** VPN (required for internal resources)
- Check that Node.js is installed: `node --version`
- Restart VS Code after configuration changes

### Configuration issues

1. Verify `mcp.json` exists in `%APPDATA%\Code\User\mcp.json`
2. Check the `content-developer.agent.md` file exists in `%APPDATA%\Code\User\prompts\`
3. Review the [Troubleshooting guide](Troubleshooting.md) for more help

---

## Next steps

- Review [Using the tools](Using-the-tools.md) to learn about all available MCP tools
- Check [Common workflows](Common-workflows.md) for step-by-step guides
- Consider [customizing your agent](Agent-customization.md) to match your work style
