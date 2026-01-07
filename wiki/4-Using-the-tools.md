# Using the tools

Complete guide to all MCP tools provided by the Content Developer Assistant.

---

## Tool categories

The Content Developer Assistant provides 10 MCP tools organized into two categories:

### Workflow tools (5 tools)

These automate your documentation workflow:

1. **[create_work_item_template](#1-create_work_item_template)** - Generate ADO work item templates
2. **[generate_git_workflow_context](#2-generate_git_workflow_context)** - Branch validation and commit messages
3. **[generate_pr_description](#3-generate_pr_description)** - PR titles and bodies with AB# linking
4. **[generate_work_item_update](#4-generate_work_item_update)** - Format progress updates
5. **[calculate_work_item_completion](#5-calculate_work_item_completion)** - Publish dates and completion comments

### Helper tools (5 tools)

These help with setup and maintenance:

6. **[complete_environment_setup](#6-complete_environment_setup)** - Authentication and git configuration
7. **[setup_repository_clone](#7-setup_repository_clone)** - Repository cloning from Learn URLs
8. **[get_workflow_example](#8-get_workflow_example)** - Step-by-step workflow examples
9. **[check_agent_version](#9-check_agent_version)** - Version checking and updates
10. **[report_bug](#10-report_bug)** - Bug reporting with system info

---

## How to use the tools

You typically don't call these tools directly. Instead, use natural language with `@content-developer-assistant`:

**Instead of**: Manually calling `create_work_item_template`  
**Say**: `@content-developer-assistant I need to create a work item`

**Instead of**: Manually calling `generate_git_workflow_context`  
**Say**: `@content-developer-assistant save my changes`

**Instead of**: Manually calling `generate_pr_description`  
**Say**: `@content-developer-assistant create a PR`

The agent orchestrates the tools and guides you through the process.

---

## 1. create_work_item_template

Generates complete ADO work item templates with auto-calculated AreaPath, IterationPath, and parent linking.

### What it does

- Calculates the correct AreaPath based on Azure service
- Determines current iteration path (e.g., "Content\\FY26\\Q3\\01 Jan")
- Links to appropriate parent work item
- Populates all required fields
- Adds "cda" tag to track Content Developer Assistant usage

### When to use

Ask the agent to create a work item:
```
@content-developer-assistant I need to create a work item
```

### What you'll be asked for

- **Title**: Brief description of the work
- **Service**: Azure service name (e.g., "ExpressRoute", "Virtual Network")
- **Workflow type**: Type of work you're doing (see below)
- **Description**: What you'll be working on
- **Assigned to**: Your email address
- **Target date** (optional): When you expect to finish

### Workflow types

Choose the workflow type that best describes your work:

- **content-maintenance** - Routine updates, freshness reviews, public PR reviews/merges
- **new-feature** - New documentation for features
- **pm-enablement** - PM-driven documentation work
- **css-support** - Customer Service and Support escalations
- **content-gap** - Filling documentation gaps
- **mvp-feedback** - MVP program feedback
- **architecture-center** - Architecture Center content
- **curation** - Content curation work

---

## 2. generate_git_workflow_context

Validates your current branch state and generates git commands for your workflow.

### What it does

- Checks if you're on the correct branch
- Determines if main branch needs syncing
- Generates unique branch names with timestamps
- Creates commit messages for each file
- Recommends branch actions (create/switch/stay)

### When to use

Ask the agent to save your changes:
```
@content-developer-assistant save my changes
```

The agent will:
1. Check your current branch
2. Ask if you need to sync main
3. Create or switch to feature branch
4. Generate commit messages for changed files
5. Ask for approval before pushing

### Branch naming

Branches are named: `{username}/{service}-{workflow-type}-{timestamp}`

Example: `duau/expressroute-content-maintenance-20260107-143052`

### Commit messages

Each file gets its own commit with a descriptive message:
```
docs: Update ExpressRoute introduction with new peering features
docs: Add private peering configuration examples
```

---

## 3. generate_pr_description

Generates pull request titles and bodies with proper AB# linking.

### What it does

- Creates descriptive PR title (without AB#)
- Generates formatted PR body with:
  - Summary of changes
  - List of files modified
  - AB#{work_item_id} linking (automatically links PR to ADO)
- Handles both new PRs and PR description updates

### When to use

Ask the agent to create a PR:
```
@content-developer-assistant create a PR
```

### AB# linking

**IMPORTANT**: AB# goes in the PR **body**, not the title.

- **Correct**: Title: "Update ExpressRoute documentation" + Body: "...AB#123456"
- **Wrong**: Title: "AB#123456 Update ExpressRoute documentation"

The AB# syntax creates automatic linking between GitHub PR and ADO work item.

---

## 4. generate_work_item_update

Generates formatted markdown progress updates for ADO work items.

### What it does

- Creates professional progress update with:
  - Date header
  - Specific accomplishments
  - Files modified (with markdown links)
  - PR links (if applicable)
  - Article URLs (if applicable)
  - Blockers (if any)
  - Next steps (if any)
- Provides best practices guidance

### When to use

Ask the agent to update your work item:
```
@content-developer-assistant update my work item with progress
```

### Best practices

**Good update** (specific):
> Updated ExpressRoute introduction article with new private peering features, added configuration examples, and updated troubleshooting section.

**Bad update** (vague):
> Updated some files.

Be specific about what you accomplished!

---

## 5. calculate_work_item_completion

Calculates publish dates and generates completion comments for closing work items.

### What it does

- Calculates next publish date (10am or 3pm PST on weekdays)
- Generates completion comment with:
  - PR reference (markdown link format)
  - Completion timestamp
  - Summary of work
- Provides fields to close work item in ADO

### When to use

After your PR is merged, ask the agent:
```
@content-developer-assistant close my work item
```

### Publish schedule

Content publishes at:
- **10:00 AM PST** (weekdays)
- **3:00 PM PST** (weekdays)

The tool automatically calculates the next available publish time.

---

## 6. complete_environment_setup

Generates authentication and git configuration commands.

### What it does

- Provides ready-to-copy authentication commands
- Generates git config with correct GitHub noreply email
- Includes verification steps
- Customized for your operating system

### When to use

**BEFORE using ADO or GitHub tools**, run:
```
@content-developer-assistant help me complete my environment setup
```

### What it configures

1. **Azure authentication**: `az login`
2. **GitHub authentication**: `gh auth login`
3. **Git configuration**:
   - User name
   - GitHub noreply email
   - Long paths (Windows)
   - VS Code as editor
   - Credential helper

---

## 7. setup_repository_clone

Generates commands to clone repositories from Learn URLs or repo names.

### What it does

- Fetches Learn page to find edit link
- Determines correct private repository (adds `-pr` suffix)
- Generates fork creation commands
- Creates shallow clone commands (`--depth 5` for speed)
- Sets up upstream remote

### When to use

Ask the agent to help you clone:
```
@content-developer-assistant help me clone https://learn.microsoft.com/en-us/azure/expressroute/expressroute-introduction
```

Or:
```
@content-developer-assistant help me clone azure-docs-pr
```

### Why shallow clone?

- Faster clone times (minutes vs hours for large repos)
- Reduced bandwidth usage
- Smaller disk space (100 MB vs 4+ GB)

---

## 8. get_workflow_example

Returns detailed step-by-step examples for specific workflows.

### What it does

- Provides complete workflow examples with:
  - MCP tool calls
  - Git commands
  - Expected outputs
  - Best practices

### When to use

When you need guidance on a specific workflow:
```
@content-developer-assistant get_workflow_example workflow_type='save-changes'
```

### Available examples

- `create-work-item` - Creating ADO work items
- `save-changes` - First save (sync main, branch, commit)
- `create-pr` - Creating PRs with AB# linking
- `save-again` - Additional commits to existing PR
- `close-work-item` - Closing after PR merge
- `session-startup` - Starting VS Code on feature branch
- `all` - Quick reference of all workflows

---

## 9. check_agent_version

Checks if your agent file is up-to-date.

### What it does

- Compares your local agent version with server version
- Provides update instructions if outdated
- Offers to download latest version
- Called automatically on first message

### When to use

The agent checks this automatically. To manually check:
```
@content-developer-assistant check my agent version
```

---

## 10. report_bug

Reports bugs to the development team with system information.

### What it does

- Creates Bug work item in ADO
- Collects system information automatically
- Assigns to development team
- Provides repro steps template

### When to use

If you encounter a bug:
```
@content-developer-assistant I found a bug - the agent created a PR with the wrong repository
```

The agent will:
1. Collect system information
2. Ask for details
3. Create bug work item
4. Provide tracking number

---

## Tool orchestration

The agent orchestrates multiple tools to complete workflows. Here's how tools work together:

### Creating a work item

1. `create_work_item_template` → Generates fields and parent link
2. `@ado-content create_work_item` → Creates work item in ADO
3. `@ado-content work_items_link` → Links to parent work item

### Saving changes

1. Check current branch with `git branch --show-current`
2. `generate_git_workflow_context` → Branch name and commit messages
3. Execute batched git commands

### Creating a PR

1. `generate_pr_description` → PR title and body with AB#
2. `@github create_pull_request` → Creates PR on GitHub

### Closing a work item

1. Fetch PR details from GitHub
2. `calculate_work_item_completion` → Publish date and completion comment
3. `@ado-content update_work_item` → Closes work item in ADO

---

## Next steps

- Review [Common workflows](Common-workflows.md) for step-by-step examples
- Learn about [Agent customization](Agent-customization.md) to tailor the agent to your needs
- Check [Troubleshooting](Troubleshooting.md) if you encounter issues
