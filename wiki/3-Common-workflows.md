# Common workflows

Step-by-step guides for typical documentation tasks using the Content Developer Assistant.

---

## Before you start

**IMPORTANT**: Complete environment setup first!

```
@content-developer-assistant help me complete my environment setup
```

This ensures you're authenticated to ADO and GitHub so the MCP servers can access those services.

---

## Workflow 1: Creating a new work item

### When to use
Starting new documentation work (feature, update, freshness review, etc.)

### Steps

1. **Ask the agent to create a work item**:
   ```
   @content-developer-assistant I need to create a work item
   ```

2. **Provide the requested information**:
   - Title: "Update ExpressRoute documentation"
   - Service: "ExpressRoute"
   - Workflow type: "content-maintenance"
   - Description: "Freshness review and feature updates"
   - Assigned to: "yourname@microsoft.com"
   - Target date: "2026-02-15" (optional)

3. **Agent creates the work item**:
   - Generates template with auto-calculated AreaPath and IterationPath
   - Creates work item in ADO
   - Links to parent work item
   - Displays work item ID (save this!)

4. **Make your documentation changes**:
   - Edit files in VS Code
   - Save your changes

---

## Workflow 2: Saving changes (first time)

### When to use
You've made changes and want to commit and push them.

### Steps

1. **Ask the agent to save**:
   ```
   @content-developer-assistant save my changes
   ```

2. **Agent checks your branch**:
   - Are you on main? → Will sync main and create feature branch
   - Are you on a feature branch? → Will use existing branch
   
3. **If syncing main is needed**:
   Agent generates and runs:
   ```bash
   git fetch upstream main
   git pull upstream main
   git push origin main
   ```

4. **Agent creates feature branch**:
   - Branch name: `{username}/{service}-{workflow-type}-{timestamp}`
   - Example: `duau/expressroute-content-maintenance-20260107-143052`

5. **Agent generates commit messages**:
   - One commit per file with descriptive message
   - Example: `docs: Update ExpressRoute introduction with new peering features`

6. **Agent asks for approval to push**:
   - Review the commits
   - Confirm to push to your fork

7. **Commits are pushed**:
   ```bash
   git checkout -b duau/expressroute-content-maintenance-20260107-143052
   git add articles/expressroute/intro.md
   git commit -m "docs: Update ExpressRoute introduction with new peering features"
   git push origin duau/expressroute-content-maintenance-20260107-143052
   ```

---

## Workflow 3: Creating a pull request

### When to use
After pushing your changes and want to create a PR.

### Steps

1. **Ask the agent to create a PR**:
   ```
   @content-developer-assistant create a PR
   ```

2. **Agent generates PR description**:
   - Title: "Update ExpressRoute documentation"
   - Body: Summary of changes + file list + AB#{work_item_id}

3. **Agent creates PR on GitHub**:
   - Creates PR against `MicrosoftDocs/azure-docs-pr` (upstream)
   - Uses your feature branch as source
   - AB# in body automatically links to ADO work item

4. **PR is created**:
   - GitHub PR URL is displayed
   - ADO work item shows linked PR
   - Work item state changes to "Active"

---

## Workflow 4: Making additional changes to existing PR

### When to use
You've created a PR but need to make more changes.

### Steps

1. **Make your additional edits**:
   - Edit files in VS Code
   - Save changes

2. **Ask the agent to save again**:
   ```
   @content-developer-assistant save my changes
   ```

3. **Agent validates context**:
   - Asks: "Are these changes related to your current branch work?"
   - If YES → Continues on current branch
   - If NO → Stashes changes, syncs main, creates new branch

4. **Agent commits and pushes**:
   - Creates new commits for changed files
   - Pushes to same branch
   - PR automatically updates

5. **Agent asks about PR description**:
   - "Would you like to update the PR description with all changes?"
   - If YES → Generates updated description with all changes
   - Updates PR description on GitHub

---

## Workflow 5: Updating work item with progress

### When to use
You want to document progress in your ADO work item.

### Steps

1. **Ask the agent to update your work item**:
   ```
   @content-developer-assistant update my work item with progress
   ```

2. **Agent generates formatted update**:
   ```markdown
   ## Progress update - January 7, 2026
   
   ### Accomplishments
   Updated ExpressRoute introduction article with new private peering features, added configuration examples, and updated troubleshooting section.
   
   ### Files modified
   - [expressroute-introduction.md](https://learn.microsoft.com/en-us/azure/expressroute/expressroute-introduction)
   - [expressroute-peering.md](https://learn.microsoft.com/en-us/azure/expressroute/expressroute-peering)
   
   ### PR
   [#12345](https://github.com/MicrosoftDocs/azure-docs-pr/pull/12345)
   
   ### Next steps
   - Address review feedback
   - Add diagrams for peering scenarios
   ```

3. **Agent adds comment to work item**:
   - Uses markdown format
   - Includes all relevant links

---

## Workflow 6: Closing a work item

### When to use
Your PR has been merged and changes are ready to publish.

### Steps

1. **Ask the agent to close your work item**:
   ```
   @content-developer-assistant close my work item
   ```

2. **Agent fetches PR details**:
   - Gets PR number, title, merge date from GitHub

3. **Agent calculates publish date**:
   - Next 10am or 3pm PST on weekdays
   - Example: "January 8, 2026 at 3:00 PM PST"

4. **Agent generates completion comment**:
   ```markdown
   ## ✅ Work completed
   
   PR [#12345](https://github.com/MicrosoftDocs/azure-docs-pr/pull/12345) merged on January 7, 2026
   
   Updated ExpressRoute introduction with new private peering features
   
   Content will publish on January 8, 2026 at 3:00 PM PST
   ```

5. **Agent closes work item**:
   - Sets state to "Closed"
   - Sets publish date in custom field
   - Adds completion comment

---

## Workflow 7: Starting VS Code on a feature branch

### When to use
You're opening VS Code and you're already on a feature branch with uncommitted changes.

### What the agent does

1. **Checks current branch**:
   ```bash
   git branch --show-current
   ```

2. **Checks for uncommitted changes**:
   ```bash
   git status --porcelain
   ```

3. **Determines action**:

   **Scenario A**: Feature branch + uncommitted changes
   - Stashes changes
   - Switches to main
   - Syncs main
   - Switches back to feature branch
   - Pops stash

   **Scenario B**: Feature branch + no changes
   - Switches to main
   - Syncs main

   **Scenario C**: Already on main
   - Syncs main

### When to trigger this

The agent automatically handles this when you say:
```
@content-developer-assistant I want to create a new work item
```

(Agent detects you're on a feature branch and handles cleanup)

---

## Workflow 8: Getting help with workflows

### When to use
You need step-by-step guidance for a specific workflow.

### Steps

1. **Ask for a workflow example**:
   ```
   @content-developer-assistant get_workflow_example workflow_type='save-changes'
   ```

2. **Agent returns detailed example**:
   - MCP tool calls with parameters
   - Git commands with explanations
   - Expected outputs
   - Best practices

3. **Available workflow types**:
   - `create-work-item` - Creating ADO work items
   - `save-changes` - First save workflow
   - `create-pr` - Creating pull requests
   - `save-again` - Additional commits
   - `close-work-item` - Closing after merge
   - `session-startup` - Session startup handling
   - `all` - Quick reference guide

---

## Workflow 9: Cloning a repository

### When to use
You need to clone an Azure documentation repository.

### Steps

1. **From a Learn article**:
   ```
   @content-developer-assistant help me clone https://learn.microsoft.com/en-us/azure/expressroute/expressroute-introduction
   ```

2. **Or by repo name**:
   ```
   @content-developer-assistant help me clone azure-docs-pr
   ```

3. **Agent determines repo**:
   - Fetches Learn page (if URL provided)
   - Finds edit link in page source
   - Converts to private repo (adds `-pr` suffix)

4. **Agent generates commands**:
   ```bash
   # Fork if you don't have one
   gh repo fork MicrosoftDocs/azure-docs-pr --remote=false
   
   # Shallow clone (faster, smaller)
   git clone --depth 5 https://github.com/yourusername/azure-docs-pr.git
   cd azure-docs-pr
   
   # Add upstream
   git remote add upstream https://github.com/MicrosoftDocs/azure-docs-pr.git
   
   # Verify
   git remote -v
   ```

5. **Copy and run commands** in your terminal

---

## Workflow 10: Reporting a bug

### When to use
You encounter a bug in the Content Developer Assistant.

### Steps

1. **Tell the agent about the bug**:
   ```
   @content-developer-assistant I found a bug - the agent created a PR with the wrong repository
   ```

2. **Agent collects system information**:
   - Runs command to get VS Code, Node.js, npm, OS versions
   - Asks for details about the bug

3. **Agent asks for details**:
   - What happened?
   - What did you expect to happen?
   - Steps to reproduce (if known)
   - How did you work around it?

4. **Agent creates bug work item**:
   - Assigns to development team
   - Includes all details and system info
   - Links to parent bug tracking item
   - Provides bug work item ID

---

## Tips for success

### General best practices

1. **Always complete environment setup first** - Run authentication commands before using ADO/GitHub tools
2. **Use descriptive titles** - Help reviewers understand your changes quickly
3. **Be specific in updates** - Document what you accomplished, not just "updated files"
4. **One commit per file** - Makes it easier to review and revert if needed
5. **Review before approving** - Always check generated commits/PR descriptions before confirming

### Working with the agent

- **Use natural language** - The agent understands conversational requests
- **Be specific** - "Create a work item for ExpressRoute freshness review" is better than "Create a work item"
- **Ask for help** - The agent can explain workflows and provide examples
- **Experiment** - Try different models (Claude Sonnet 4.5 recommended but experiment!)

### Common mistakes to avoid

- ❌ **Skipping authentication** - MCP servers need az/gh login
- ❌ **Putting AB# in PR title** - AB# goes in PR body only
- ❌ **Vague work item updates** - Be specific about accomplishments
- ❌ **Not syncing main** - Always sync main before creating new branch
- ❌ **Committing to main directly** - Always use feature branches

---

## Next steps

- Learn about [customizing your agent](Agent-customization.md) to match your workflow
- Review [Using the tools](Using-the-tools.md) for detailed tool documentation
- Check [Troubleshooting](Troubleshooting.md) if you encounter issues
