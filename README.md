# Content Developer Agent - Quick setup

This folder contains the essential files needed to get started with the Content Developer Assistant.

## Files

- **Content Developer Setup.exe** - Automated installer (recommended for first-time setup)
- **mcp.json** - MCP server configuration for VS Code
- **content-developer.agent.md** - Baseline agent instructions for creating ADO work items, operating git commands, and creating PRs

**Note**: The content-developer agent is a starting point. Once you're familiar with how agents work, you're encouraged to create your own custom agent tailored to your specific work style and preferences.

## Quick setup instructions

### Option 1: Automated installation (recommended)

Simply run **Content Developer Setup.exe** - it will:
- Install all required tools (VS Code, Git, Node.js, Azure CLI, GitHub CLI)
- Configure MCP servers automatically
- Download the latest agent file
- Set up your user profile

This is the easiest way to get started!

### Option 2: Manual setup

If you prefer manual setup or already have some tools installed:

#### 1. Install prerequisites

First, install the required tools:
- [VS Code](https://code.visualstudio.com/)
- [Git](https://git-scm.com/downloads)
- [Node.js](https://nodejs.org/)
- [Azure CLI](https://learn.microsoft.com/cli/azure/install-azure-cli)
- [GitHub CLI](https://cli.github.com/)

#### 2. Configure MCP servers

**Option A: Copy to VS Code user settings**
```bash
# Windows
copy mcp.json %APPDATA%\Code\User\mcp.json

# Mac/Linux
cp mcp.json ~/Library/Application\ Support/Code/User/mcp.json
```

**Option B: Manual setup**
1. Open VS Code Settings (Ctrl+,)
2. Search for "MCP"
3. Click "Edit in settings.json"
4. Copy the contents of `mcp.json` into the appropriate section

**Important**: Edit the `content-developer-assistant` server headers with your information:
```json
"headers": {
  "X-User-Name": "Your Full Name",
  "X-User-Alias": "youralias",
  "X-User-Role": "Content Developer"
}
```

#### 3. Install agent file

**Option A: Copy to VS Code prompts directory**
```bash
# Windows
copy content-developer.agent.md %APPDATA%\Code\User\prompts\content-developer.agent.md

# Mac/Linux
cp content-developer.agent.md ~/Library/Application\ Support/Code/User/prompts/content-developer.agent.md
```

**Option B: Download latest**
```bash
curl http://roguereporting2:8000/agent > content-developer.agent.md
```

#### 4. Complete authentication and agent setup

After restarting VS Code:

1. **Sign in to GitHub Copilot** (bottom right status bar)
2. **Select the model**: Click the model selector in Copilot Chat and choose **Claude Sonnet 4.5** (recommended, but feel free to experiment with other models)
3. **Activate agent mode**: In Copilot Chat settings, select **content-developer** as your agent mode
4. Open GitHub Copilot Chat
5. Type `@content-developer-assistant` to verify the agent is loaded
6. Complete environment setup:
   ```
   @content-developer-assistant help me complete my environment setup
   ```

This will guide you through:
- Azure authentication (`az login`)
- GitHub authentication (`gh auth login`)
- Git configuration

## Troubleshooting

**Agent not showing up?**
- Verify you're signed into GitHub Copilot (bottom right status bar)
- Restart VS Code
- Check that mcp.json exists in `%APPDATA%\Code\User\`
- Check that the agent file exists in `%APPDATA%\Code\User\prompts\`

**MCP servers not working?**
- Verify you've run `az login` and `gh auth login`
- Check that Node.js is installed: `node --version`
- Restart VS Code after configuration changes

## Updating

To get the latest agent file:
```bash
curl http://roguereporting2:8000/agent > content-developer.agent.md
```

Then copy it to your VS Code prompts directory.

## Which setup method should I use?

- **New to Content Developer tools?** → Use **Content Developer Setup.exe** (automated installer)
- **Already have tools installed?** → Use manual setup (copy mcp.json and agent file)
- **Want full control?** → Use manual setup
- **Prefer one-click solution?** → Use **Content Developer Setup.exe**

## Full installation

For a complete automated installation, use the [Content Developer Installer](../content-developer-installer).

## Documentation

For comprehensive guides and documentation, see the [wiki](wiki/README.md):

- **[Getting started](wiki/Getting-started.md)** - Installation and first-time setup
- **[Using the tools](wiki/Using-the-tools.md)** - Complete guide to all MCP tools
- **[Common workflows](wiki/Common-workflows.md)** - Step-by-step examples
- **[Agent customization](wiki/Agent-customization.md)** - Personalize the agent
- **[Troubleshooting](wiki/Troubleshooting.md)** - Solutions to common issues

## Support

For issues or questions, contact the Content Developer team or file an issue in the repository.
