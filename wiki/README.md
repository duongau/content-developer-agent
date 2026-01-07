# Content Developer Assistant Wiki

Welcome to the Content Developer Assistant documentation!

---

## What's inside

This wiki provides comprehensive guidance for using the Content Developer Assistant to automate your Azure documentation workflows.

### 📖 Documentation pages

1. **[Home](Home.md)** - Overview and quick start
2. **[Getting started](Getting-started.md)** - Installation, setup, and first steps
3. **[Using the tools](Using-the-tools.md)** - Complete guide to all 10 MCP tools
4. **[Common workflows](Common-workflows.md)** - Step-by-step guides for typical tasks
5. **[Agent customization](Agent-customization.md)** - How to customize the agent for your work style
6. **[Troubleshooting](Troubleshooting.md)** - Solutions to common issues

---

## Quick navigation

### New users

Start here:
1. [Getting started](Getting-started.md) - Install and set up
2. Complete environment setup (run authentication)
3. [Common workflows](Common-workflows.md) - Learn your first workflow

### Experienced users

- [Using the tools](Using-the-tools.md) - Reference for specific tools
- [Agent customization](Agent-customization.md) - Tailor the agent to your needs
- [Troubleshooting](Troubleshooting.md) - Fix common issues

---

## Before you start

**CRITICAL**: Complete environment setup before using ADO/GitHub tools!

```
@content-developer-assistant help me complete my environment setup
```

This authenticates you to:
- Azure DevOps (for work item management)
- GitHub (for PR management)
- Git configuration

Without this, the MCP servers cannot access ADO and GitHub on your behalf.

---

## What you'll learn

### Installation and setup
- How to install the Content Developer Assistant
- Configuring agent mode and model selection
- Authentication setup for ADO and GitHub
- Cloning your first repository

### Using the tools
- Creating ADO work items with auto-calculated fields
- Managing git operations (branching, committing, pushing)
- Creating pull requests with AB# linking
- Updating and closing work items
- Getting workflow examples and help

### Advanced topics
- Customizing the agent file for your work style
- Adding team-specific conventions
- Modifying PR templates and commit styles
- Troubleshooting common issues

---

## Key concepts

### MCP tools
10 specialized tools that automate documentation workflows:
- 5 workflow tools (work items, git, PRs, updates, completion)
- 5 helper tools (setup, cloning, examples, version, bugs)

### Agent file
Markdown file (`content-developer.agent.md`) that contains instructions for how the AI should behave. It's a **baseline** you can customize.

### Workflow orchestration
The agent orchestrates multiple MCP tools to complete complex tasks. You use natural language, the agent calls the tools.

### Integration
Works with other MCP servers:
- `@ado-content` - Azure DevOps API execution
- `@github` - GitHub API execution
- `@microsoft-docs` - Microsoft Learn documentation search

---

## Getting help

### In the wiki
- Check [Troubleshooting](Troubleshooting.md) for common issues
- Review [Common workflows](Common-workflows.md) for step-by-step examples
- Read [Using the tools](Using-the-tools.md) for tool details

### From the agent
Ask the agent directly:
```
@content-developer-assistant get_workflow_example workflow_type='all'
@content-developer-assistant How do I [specific task]?
@content-developer-assistant I'm stuck with [problem]
```

### Report bugs
```
@content-developer-assistant I found a bug - [describe issue]
```

### Contact support
- Your team lead
- Your team's Teams channel
- File an issue in the repository

---

## Contributing

Found an error or want to improve the documentation?

1. File an issue or PR in the repository
2. Share feedback with your team
3. Suggest improvements to the agent customization

---

## Version information

**Wiki version**: 1.0.0  
**Agent version**: 5.5.2  
**Last updated**: January 2026

For the latest agent file:
```bash
curl http://roguereporting2:8000/agent > content-developer.agent.md
```

---

## Quick reference

### Essential commands

**Setup**:
```
@content-developer-assistant help me complete my environment setup
@content-developer-assistant help me clone [Learn URL or repo name]
```

**Workflows**:
```
@content-developer-assistant I need to create a work item
@content-developer-assistant save my changes
@content-developer-assistant create a PR
@content-developer-assistant update my work item with progress
@content-developer-assistant close my work item
```

**Help**:
```
@content-developer-assistant get_workflow_example workflow_type='all'
@content-developer-assistant check my agent version
@content-developer-assistant I found a bug - [description]
```

---

## Next steps

1. **Install**: Run `Content Developer Setup.exe` or follow manual setup
2. **Authenticate**: Complete environment setup
3. **Learn**: Read [Getting started](Getting-started.md)
4. **Practice**: Try [Common workflows](Common-workflows.md)
5. **Customize**: Personalize your [agent](Agent-customization.md)

Happy documenting! 🚀
