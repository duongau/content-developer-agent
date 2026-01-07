# Agent customization

Learn how to customize the Content Developer agent to match your personal work style.

---

## Understanding the agent file

The `content-developer.agent.md` file is a **baseline agent** that provides:

- Work item creation automation
- Git workflow management  
- Pull request creation
- Work item progress tracking

**It's designed as a starting point**, not a one-size-fits-all solution.

---

## Why customize your agent?

Everyone works differently. You might want to:

- **Change the tone** - More formal, more casual, more technical
- **Add shortcuts** - Custom commands for your frequent tasks
- **Modify workflows** - Adjust branching strategy, commit style, PR templates
- **Add team-specific rules** - Your team's conventions and requirements
- **Integrate other tools** - Add support for additional MCP servers or tools

---

## How agents work

Agents are markdown files that contain instructions for how the AI should behave. The agent file tells the AI:

1. **Who it is** - Role and expertise
2. **What it can do** - Available tools and capabilities  
3. **How to respond** - Workflow patterns and best practices
4. **When to use tools** - Triggers and conditions

When you use `@content-developer-assistant`, the AI reads the agent file and follows those instructions.

---

## Getting started with customization

### Step 1: Make a copy

Create your own agent file:

```bash
# Copy the baseline
copy "%APPDATA%\Code\User\prompts\content-developer.agent.md" "%APPDATA%\Code\User\prompts\my-custom.agent.md"

# Or on Mac/Linux
cp ~/Library/Application\ Support/Code/User/prompts/content-developer.agent.md ~/Library/Application\ Support/Code/User/prompts/my-custom.agent.md
```

### Step 2: Activate your agent mode

1. Open VS Code settings
2. Search for "agent mode" or "chat mode"
3. Create a new agent mode pointing to your custom file
4. Select your custom agent in Copilot Chat

### Step 3: Start customizing

Edit your `my-custom.agent.md` file with your preferences.

---

## Customization examples

### Example 1: Change the commit message style

**Default**:
```
docs: Update ExpressRoute introduction with new peering features
```

**Custom (more detailed)**:

Find the git workflow section in your agent file and modify:

```markdown
### Commit message format

Generate detailed commit messages with:
- **Type**: docs, feat, fix, style, refactor
- **Scope**: File or section name
- **Subject**: Imperative mood, detailed description
- **Body**: Multi-line explanation of changes (optional)

Example:
```
docs(expressroute): update introduction with private peering features

- Added detailed explanation of private peering configuration
- Included diagrams for peering scenarios
- Updated prerequisites section with new requirements
```
```

### Example 2: Add custom workflow shortcuts

Add to your agent file:

```markdown
## Custom commands

### Quick freshness review
When user says "start freshness review for [service]":
1. Create work item with workflow_type="content-maintenance"
2. Title: "[Service] - Q[quarter] FY[year] freshness review"
3. Auto-populate description with freshness review checklist
4. Clone repository if not already cloned
5. Open relevant articles in VS Code

### Quick PR merge
When user says "merge and close [work_item_id]":
1. Verify PR is approved
2. Merge PR on GitHub
3. Calculate publish date
4. Close work item with completion comment
5. Notify team in Teams (if configured)
```

### Example 3: Customize PR templates

Modify the PR description generation:

```markdown
### PR description template

Generate PR descriptions with this structure:

```markdown
## 📝 Summary
[Brief overview of changes]

## 🎯 Work item
AB#[work_item_id]

## 📋 Changes
- [Specific change 1]
- [Specific change 2]

## 🧪 Validation
- [ ] Local build successful
- [ ] All links verified
- [ ] Images render correctly
- [ ] Acrolinx score > 80

## 📚 Related articles
- [Link to related doc 1]
- [Link to related doc 2]
```
```

### Example 4: Add team-specific conventions

Add your team's requirements:

```markdown
## Team conventions (Azure Networking)

### Required PR reviewers
Always add these reviewers to PRs:
- Technical reviewer: @team-tech-lead
- Content reviewer: @team-content-lead

### Article naming conventions
- Use lowercase with hyphens: `virtual-network-overview.md`
- Include service prefix: `vnet-peering-configuration.md`

### Tagging requirements
Work items must include:
- Service tag (e.g., "Virtual Network")
- "cda" tag (auto-added by agent)
- Team tag: "azure-networking"

### Build validation
Before creating PR, verify:
1. `npm run build` succeeds
2. No Acrolinx errors (warnings OK)
3. All images < 1MB
4. No broken links
```

### Example 5: Modify the agent's personality

Change how the agent communicates:

```markdown
## Communication style

**Tone**: Professional yet friendly, like a helpful senior colleague

**Principles**:
- Be concise but complete
- Explain "why" not just "what"
- Offer tips and best practices
- Anticipate questions
- Use analogies when explaining complex concepts

**Example interactions**:

❌ **Too terse**: "Created work item 123456."

✅ **Better**: "I've created work item 123456 for your ExpressRoute freshness review. Since this is a quarterly review, I've set the iteration to Q3 and linked it to the FY26 planning epic. Ready to start making changes?"

**When user makes a mistake**:

❌ **Blaming**: "You can't commit to main."

✅ **Helpful**: "Looks like you're on the main branch. Let me help you create a feature branch to keep main clean for team syncs. What would you like to name your branch?"
```

---

## Advanced customizations

### Adding support for additional MCP servers

If your team uses other MCP servers:

```markdown
## Additional MCP servers

### Using the learning paths server
When working on learning modules:
1. Use @learning-paths to search existing modules
2. Use @content-developer-assistant to manage work items and git workflow

### Using the Azure API server
For API documentation:
1. Use @azure-api to fetch API definitions
2. Use @content-developer-assistant to create documentation from specs
```

### Conditional workflows

Add logic for different scenarios:

```markdown
## Conditional workflows

### If working on quickstarts
- Use minimal commit messages
- Skip Acrolinx validation (quickstarts are code-heavy)
- Add "quickstart" tag to work items

### If working on tutorials
- Require detailed commit messages
- Mandate Acrolinx score > 85
- Include "tutorial" tag and learning path link

### If working on reference docs
- Auto-generate from code comments when possible
- Link to GitHub source files
- Add "reference" tag
```

---

## Testing your customizations

### 1. Test incrementally

- Make one change at a time
- Test thoroughly before adding more
- Keep a backup of working versions

### 2. Validate with real workflows

Test your customizations with actual tasks:
- Create a work item
- Make changes and commit
- Create a PR
- Update and close work item

### 3. Get feedback

Share with teammates:
- What works well?
- What's confusing?
- What's missing?

---

## Best practices

### Do's

✅ **Start small** - Customize one section at a time  
✅ **Document changes** - Add comments explaining why you made each change  
✅ **Version your agent** - Keep backups of working versions  
✅ **Share with team** - If something works well, share it  
✅ **Iterate** - Refine based on real usage  

### Don'ts

❌ **Don't remove core workflows** - Keep work item creation, git, PR management  
❌ **Don't overcomplicate** - Simple is better than complex  
❌ **Don't break compatibility** - Ensure MCP tools still work  
❌ **Don't hardcode values** - Use parameters instead  
❌ **Don't forget updates** - Check for new agent versions periodically  

---

## Example: Full custom agent template

Here's a skeleton for creating your own agent from scratch:

```markdown
# My Custom Documentation Agent

**Version**: 1.0.0
**Based on**: Content Developer Agent v5.5.2
**Customizations**: [Your team name] conventions

---

## About me

I'm your personalized documentation assistant, specialized in:
- [Your specific domain/service]
- [Your team's workflow]
- [Your tools/systems]

---

## My capabilities

[List what you can do - based on MCP tools + your additions]

---

## How I work

### Creating work items
[Your customized workflow]

### Managing git operations
[Your customized git workflow]

### Creating pull requests
[Your customized PR workflow]

### Your custom workflows
[Additional workflows you've added]

---

## Team conventions

[Your team-specific rules and requirements]

---

## Communication style

[How you want the agent to communicate]

---

## Integration points

[Other systems/tools you integrate with]
```

---

## Sharing your customizations

If you create valuable customizations:

1. **Document them** - Write clear explanations
2. **Share with team** - Help teammates benefit
3. **Contribute back** - Consider sharing with broader community
4. **Get feedback** - Learn from others' experiences

---

## Getting help with customization

- Review the baseline `content-developer.agent.md` for examples
- Check the [Using the tools](Using-the-tools.md) guide for MCP tool capabilities
- Ask the agent: `@content-developer-assistant How can I customize [specific aspect]?`
- Experiment with different models (Claude, GPT-4, etc.) to see what works best

---

## Next steps

- Start with small customizations
- Test thoroughly with real workflows
- Gather feedback from your workflow
- Share successful patterns with your team
- Keep your agent updated with new features
