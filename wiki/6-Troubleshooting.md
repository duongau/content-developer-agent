# Troubleshooting

Solutions to common issues with the Content Developer Assistant.

---

## Quick fixes

Before troubleshooting specific issues, try these:

1. **Restart VS Code** - Solves most configuration issues
2. **Check VPN connection** - Connect to MSFT-AzVPN-Manual for internal resources
3. **Verify authentication** - Run `az login` and `gh auth login`
4. **Check Copilot sign-in** - Look for GitHub Copilot icon in bottom-right status bar

---

## Agent not visible in Copilot Chat

**Symptom**: Typing `@` in Copilot Chat doesn't show `@content-developer-assistant`

### Solution 1: Sign into GitHub Copilot (Most common!)

**This is the #1 reason agents don't appear.**

1. Look at the **bottom-right status bar** in VS Code
2. Find the GitHub Copilot icon
3. Click and sign in with your GitHub account
4. **Restart VS Code**
5. Open Copilot Chat and type `@` to verify

### Solution 2: Verify agent mode is selected

1. Open Copilot Chat settings
2. Check if **content-developer** agent mode is selected
3. If not visible, verify agent file exists:
   - Windows: `%APPDATA%\Code\User\prompts\content-developer.agent.md`
   - Mac: `~/Library/Application Support/Code/User/prompts/content-developer.agent.md`

### Solution 3: Check MCP configuration

1. Verify `mcp.json` exists:
   - Windows: `%APPDATA%\Code\User\mcp.json`
   - Mac: `~/Library/Application Support/Code/User/mcp.json`

2. Open the file and verify it has the `content-developer-assistant` server entry

3. Check for JSON syntax errors (common: trailing commas, missing quotes)

### Solution 4: Reinstall agent file

Download the latest agent file:

```bash
# Windows
curl http://roguereporting2:8000/agent > "%APPDATA%\Code\User\prompts\content-developer.agent.md"

# Mac/Linux
curl http://roguereporting2:8000/agent > ~/Library/Application\ Support/Code/User/prompts/content-developer.agent.md
```

Restart VS Code after downloading.

---

## MCP servers not working

**Symptom**: Agent responds but ADO/GitHub tools fail

### Solution 1: Complete authentication

**IMPORTANT**: You must authenticate before using ADO/GitHub tools.

Run these commands in your terminal:

```bash
# Azure DevOps authentication
az login

# GitHub authentication
gh auth login
```

Verify authentication:
```bash
# Check Azure
az account show

# Check GitHub
gh auth status
```

### Solution 2: Check VPN connection

The MCP server and Azure DevOps require VPN:

1. Connect to **MSFT-AzVPN-Manual**
2. Verify connection
3. Try the agent again

### Solution 3: Verify Node.js is installed

MCP servers require Node.js:

```bash
node --version
```

Should return v18 or later. If not installed:
- Windows: Download from nodejs.org
- Run the installer again

### Solution 4: Check MCP server headers

Verify your user information is configured in `mcp.json`:

```json
"content-developer-assistant": {
  "headers": {
    "X-User-Name": "Your Full Name",
    "X-User-Alias": "youralias",
    "X-User-Role": "Content Developer"
  }
}
```

Update with your actual information.

---

## "Permission denied" or "Unauthorized" errors

**Symptom**: Tools fail with permission or authorization errors

### Solution 1: Re-authenticate

```bash
# Clear Azure CLI cache
az account clear

# Re-login
az login

# Clear GitHub CLI auth
gh auth logout
gh auth login
```

### Solution 2: Check organization access

Verify you have access to the required Azure DevOps organizations:

1. Open https://dev.azure.com
2. Check if you see:
   - **msft-skilling** (for Content org work items)
   - **supportability** (if you're a Technical Advisor)

If not visible, request access from your team lead.

### Solution 3: Verify GitHub access

Check you have access to MicrosoftDocs repositories:

```bash
gh repo view MicrosoftDocs/azure-docs-pr
```

If denied, verify:
- You're a member of the MicrosoftDocs organization
- You have the correct repository permissions

---

## Work item creation fails

**Symptom**: Agent generates template but work item isn't created in ADO

### Solution 1: Check ADO authentication

```bash
az login
az account show
```

Verify you're logged into the correct account.

### Solution 2: Verify service name

Common issue: Service name doesn't match Azure service catalog.

**Correct**: "ExpressRoute", "Virtual Network", "Application Gateway"  
**Wrong**: "Express Route", "VNet", "App Gateway"

Use the exact Azure service name from https://azure.microsoft.com/products/.

### Solution 3: Check AreaPath

If you see "AreaPath not found" errors:

1. Verify the service exists in ADO
2. Check the team area path structure
3. Contact your team lead if the service should exist

---

## Git operations fail

**Symptom**: Branch creation, commits, or pushes fail

### Solution 1: Configure git

Run the complete environment setup:

```
@content-developer-assistant help me complete my environment setup
```

This configures:
- User name
- Email (GitHub noreply)
- Credential helper
- Long paths (Windows)

### Solution 2: Check remote configuration

```bash
git remote -v
```

Should show:
```
origin    https://github.com/yourusername/azure-docs-pr.git (fetch)
origin    https://github.com/yourusername/azure-docs-pr.git (push)
upstream  https://github.com/MicrosoftDocs/azure-docs-pr.git (fetch)
upstream  https://github.com/MicrosoftDocs/azure-docs-pr.git (push)
```

If missing upstream:
```bash
git remote add upstream https://github.com/MicrosoftDocs/azure-docs-pr.git
```

### Solution 3: Check GitHub authentication

```bash
gh auth status
```

Should show you're logged in. If not:
```bash
gh auth login
```

### Solution 4: Sync main branch

If pushes fail due to branch behind:

```bash
git fetch upstream main
git pull upstream main
git push origin main
```

---

## PR creation fails

**Symptom**: Agent generates PR description but PR isn't created

### Solution 1: Check GitHub CLI authentication

```bash
gh auth status
```

Re-authenticate if needed:
```bash
gh auth logout
gh auth login
```

### Solution 2: Verify branch is pushed

Before creating PR, ensure your branch is pushed:

```bash
git push origin your-branch-name
```

### Solution 3: Check repository permissions

Verify you can create PRs in the repository:

```bash
gh pr list --repo MicrosoftDocs/azure-docs-pr
```

If this fails, you may not have permissions.

---

## Agent gives unexpected responses

**Symptom**: Agent doesn't follow expected workflow or gives strange responses

### Solution 1: Verify correct agent is active

1. Check agent mode is set to **content-developer**
2. Verify you're using `@content-developer-assistant` in your messages

### Solution 2: Check agent file version

```
@content-developer-assistant check my agent version
```

Update if outdated:
```bash
curl http://roguereporting2:8000/agent > "%APPDATA%\Code\User\prompts\content-developer.agent.md"
```

### Solution 3: Try different model

The agent works best with **Claude Sonnet 4.5**, but you can experiment:

1. Click model selector in Copilot Chat
2. Try Claude Sonnet 4.5, GPT-4, or other models
3. See which works best for your workflow

### Solution 4: Provide more context

The agent works better with specific requests:

❌ **Too vague**: "Create a work item"  
✅ **Better**: "Create a work item for ExpressRoute freshness review"

❌ **Too vague**: "Save changes"  
✅ **Better**: "Save my changes to articles/expressroute/intro.md and peering.md"

---

## Performance issues

**Symptom**: Agent responses are slow or timeout

### Solution 1: Check network connection

- Verify VPN is connected
- Test internet speed
- Check for network issues

### Solution 2: Reduce parallel operations

If running multiple git/ADO/GitHub operations:
- Let each operation complete before starting next
- Don't run multiple agent requests simultaneously

### Solution 3: Clear VS Code cache

```bash
# Close VS Code
# Delete cache folder
# Windows
rd /s /q "%APPDATA%\Code\Cache"

# Mac
rm -rf ~/Library/Application\ Support/Code/Cache
```

Restart VS Code.

---

## Common error messages

### "Cannot read property 'servers' of undefined"

**Cause**: `mcp.json` is malformed or empty

**Solution**: Copy a fresh `mcp.json` from the content-developer-agent folder

---

### "ENOTFOUND roguereporting2"

**Cause**: Not connected to VPN or DNS issue

**Solution**: 
1. Connect to MSFT-AzVPN-Manual
2. Run `ping roguereporting2` to verify

---

### "Git command failed: fatal: not a git repository"

**Cause**: VS Code opened in non-git folder

**Solution**: 
1. Clone repository first
2. Open VS Code in the repository folder

---

### "Work item validation failed: AreaPath not found"

**Cause**: Service name doesn't exist in ADO team structure

**Solution**: 
1. Verify service name spelling
2. Check with team lead if service should exist
3. Use existing service name temporarily

---

### "AB# syntax did not create link"

**Cause**: AB# might be in wrong location or format

**Solution**:
- AB# must be in PR **body**, not title
- Format: `AB#123456` (no spaces)
- Must be a valid work item ID
- Work item must exist in correct ADO org

---

## Still having issues?

### Collect diagnostic information

1. **Check VS Code version**:
   ```
   Help > About
   ```

2. **Check agent version**:
   ```
   @content-developer-assistant check my agent version
   ```

3. **Check installed tools**:
   ```bash
   code --version
   node --version
   git --version
   az --version
   gh --version
   ```

4. **Check MCP configuration**:
   ```bash
   # Windows
   type "%APPDATA%\Code\User\mcp.json"
   
   # Mac/Linux
   cat ~/Library/Application\ Support/Code/User/mcp.json
   ```

### Report a bug

If you've found a bug in the agent:

```
@content-developer-assistant I found a bug - [describe the issue]
```

The agent will:
1. Collect system information
2. Ask for details
3. Create a bug work item
4. Assign to development team

### Get help

- Contact your team lead
- Ask in your team's Teams channel
- File an issue in the repository
- Review the [Common workflows](Common-workflows.md) guide

---

## Prevention tips

Avoid common issues by:

1. **Always run authentication first** - `az login` and `gh auth login` before starting work
2. **Keep tools updated** - Check for updates regularly
3. **Use VPN** - Connect to MSFT-AzVPN-Manual when working
4. **Restart VS Code** - After configuration changes
5. **Sync main regularly** - Before creating new branches
6. **Test workflows** - Verify setup with simple operations first

---

## Next steps

- Review [Getting started](Getting-started.md) for setup guidance
- Check [Common workflows](Common-workflows.md) for step-by-step examples
- Learn about [Using the tools](Using-the-tools.md) for detailed tool documentation
