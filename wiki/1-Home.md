# Content Developer Assistant

**Purpose**: Streamline Azure documentation workflows with automated work item management, git operations, and PR creation

---

## Welcome

This wiki provides comprehensive guidance for using the Content Developer Assistant, including the MCP tools and agent file that help automate your documentation workflow.

### What you'll find here

- **[Getting started](Getting-started.md)** - Installation, setup, and first steps
- **[Using the tools](Using-the-tools.md)** - Guide to all MCP tools and how to use them
- **[Common workflows](Common-workflows.md)** - Step-by-step guides for typical tasks
- **[Agent customization](Agent-customization.md)** - How to customize the agent for your work style
- **[Troubleshooting](Troubleshooting.md)** - Solutions to common issues

---

## Quick start

1. **Install** - Run `Content Developer Setup.exe` or follow manual setup instructions
2. **Authenticate** - Complete environment setup to connect to ADO and GitHub
3. **Start working** - Use the agent to create work items, manage git operations, and create PRs

---

## What is the Content Developer Assistant?

The Content Developer Assistant consists of:

### 1. MCP tools (10 tools)

**Workflow tools** - Automate your documentation workflow:
- Create ADO work items with auto-calculated fields
- Generate git branch names and commit messages
- Create pull requests with proper AB# linking
- Format work item progress updates
- Calculate publish dates and close work items

**Helper tools** - Get started and stay up-to-date:
- Complete environment setup guide
- Repository cloning from Learn URLs
- Workflow examples and guidance
- Version checking and bug reporting

### 2. Agent file (content-developer.agent.md)

A baseline agent that orchestrates the MCP tools to:
- Guide you through work item creation
- Automate git operations (branching, committing, pushing)
- Create PRs against upstream repositories
- Update and close work items

**Note**: The agent file is a starting point. Once familiar with how agents work, you can create your own custom agent tailored to your specific work style.

---

## Integration with other MCP servers

The Content Developer Assistant works with:

- **@ado-content** - Azure DevOps work item management (executes API calls)
- **@github** - GitHub PR management (executes API calls)
- **@microsoft-docs** - Microsoft Learn documentation search

**Pattern**: `@content-developer-assistant` generates business logic (AreaPath, branch names, commit messages) → Other servers execute API calls

---

## Support

For issues or questions:
- Check the [Troubleshooting](Troubleshooting.md) guide
- Contact your team lead
- File an issue in the repository
