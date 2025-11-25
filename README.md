# JIRA Workflow Management System

A comprehensive Claude Code command system for managing software development workflows through Atlassian JIRA and Confluence integration.

## Overview

This project provides a set of custom Claude Code slash commands that enable systematic planning, task breakdown, and execution of software development work through JIRA and Confluence. It automates the entire lifecycle from ideation to implementation, ensuring traceability and quality throughout the development process.

## Features

### Planning Commands (`/plan`)

- **`/plan:brainstorm`** - Critical thinking partner for validating ideas and defining requirements
  - Challenges assumptions and validates real problems
  - Generates solution alternatives
  - Outputs clear problem statements and recommendations

- **`/plan:prd`** - Creates comprehensive Product Requirements Documents in Confluence
  - Performs market research based on project type
  - Documents functional and non-functional requirements
  - Establishes success metrics and risk assessment

- **`/plan:feature`** - Creates focused technical feature documents in Confluence
  - Adapts to project context (Web, API, CLI, etc.)
  - Documents system impact and integration requirements
  - Defines acceptance criteria and success metrics

- **`/plan:tasks`** - Breaks down PRDs/features into implementable JIRA task issues
  - Creates hierarchically numbered task structure
  - Establishes task dependencies and critical path
  - Links all tasks to parent Confluence documentation

### Execution Commands (`/do`)

- **`/do:task`** - Executes a specific JIRA task issue with systematic implementation
  - Fetches task details and analyzes requirements
  - Creates feature branch and updates JIRA status
  - Implements with test-first development approach
  - Validates quality and updates documentation

- **`/do:changelog`** - Updates CHANGELOG.md with version entries
  - Follows Keep a Changelog conventions
  - Supports all standard change types

- **`/do:commit`** - Creates conventional commits for staged changes
  - Analyzes git diff and suggests 3-5 commit message options
  - Follows conventional commit format (type(scope): description)
  - Ensures consistent commit message standards

- **`/do:pr`** - Creates pull requests with structured format
  - Links to JIRA task and Confluence documentation
  - Includes detailed summary and file changes
  - Provides test plan and context

## Prerequisites

Before using this workflow system, you need:

1. **Claude Code** - Install from [claude.com/claude-code](https://claude.com/claude-code)
2. **Atlassian Account** - Access to JIRA and Confluence
3. **Git** - Version control for your projects
4. **Node.js** (optional) - For MCP server installation via npx

## Installation

### Step 1: Clone this Repository

```bash
git clone https://github.com/jonbito/jira-workflow.git
cd jira-workflow
```

### Step 2: Install the commands

#### Method 1: Global Install

Install commands globally to use them in any project:

```bash
# Copy commands to Claude Code's global commands directory
cp -r .claude/commands/* ~/.claude/commands/
```

#### Method 2: Local Install (Per Project)

Install commands locally to a specific project:

```bash
# Navigate to your project directory
cd /path/to/your/project

# Copy the entire .claude directory
cp -r /path/to/jira-workflow/.claude .

# Or copy just the commands
mkdir -p .claude/commands
cp -r /path/to/jira-workflow/.claude/commands/* .claude/commands/
```

### Step 3: Install the Atlassian Rovo MCP Server

The Atlassian Rovo MCP (Model Context Protocol) server enables Claude Code to interact with JIRA and Confluence using Atlassian Rovo.

Docs: <https://support.atlassian.com/atlassian-rovo-mcp-server/docs/setting-up-claude-ai/>

```bash
claude mcp add --transport sse atlassian https://mcp.atlassian.com/v1/sse
```

### Step 4: Authenticate with Atlassian

1. Start Claude Code in your project directory
2. When you first use an Atlassian MCP tool, you'll be prompted to authenticate
3. Claude will provide an authentication URL
4. Open the URL in your browser and authorize Claude Code to access your Atlassian site
5. The authentication is handled automatically through the Rovo server - no manual OAuth configuration needed

### Step 5: Install the GitHub MCP Server

Docs: <https://github.com/github/github-mcp-server/blob/main/docs/installation-guides/install-claude.md>

```bash
claude mcp add --transport http github https://api.githubcopilot.com/mcp -H "Authorization: Bearer YOUR_GITHUB_PAT"
```

## Usage

### Typical Development Workflow

#### 1. Brainstorm and Validate Ideas

```
/plan:brainstorm I need a way to track user activity across sessions
```

This command will:

- Challenge your assumptions
- Validate the real problem
- Generate solution alternatives
- Provide a clear recommendation

#### 2. Create a Feature Document

```
/plan:feature User activity tracking system
```

This creates a Confluence page with:

- Technical requirements
- System impact analysis
- Acceptance criteria
- Implementation approach

#### 3. Break Down into Tasks

```
/plan:tasks https://yoursite.atlassian.net/wiki/spaces/SPACE/pages/123456789
```

This creates JIRA task issues:

- Hierarchically numbered (1, 2.1, 2.2, 3.1, etc.)
- Linked to parent Confluence doc
- With clear dependencies and critical path

#### 4. Execute Tasks

```
/do:task PROJECT-123
```

This implements the task:

- Creates feature branch
- Updates JIRA status to "In Progress"
- Implements with test-first approach
- Runs tests and validation
- Updates documentation

#### 5. Commit Changes

```
/do:commit
```

This creates a conventional commit:

- Analyzes your staged changes
- Suggests 3-5 commit message options
- Formats according to conventional commits standard
- Creates the commit with your selected option

#### 6. Create Pull Request

```
/do:pr
```

This creates a structured PR:

- Links to JIRA task and Confluence documentation
- Includes summary of changes
- Lists modified and new files
- Provides test plan and context

#### 7. Track Changes

```
/do:changelog 1.2.0 added user activity tracking
```

### Alternative: Start with a PRD

For larger initiatives, start with a comprehensive PRD:

```
/plan:prd Multi-tenant user management system
```

Then follow steps 3-7 above.

## Command Reference

### Planning Commands

| Command            | Purpose                     | Input               | Output                             |
| ------------------ | --------------------------- | ------------------- | ---------------------------------- |
| `/plan:brainstorm` | Validate and refine ideas   | Problem description | Problem statement + recommendation |
| `/plan:prd`        | Create product requirements | Feature name        | Confluence PRD page                |
| `/plan:feature`    | Create technical feature    | Feature description | Confluence feature page            |
| `/plan:tasks`      | Break down into tasks       | Confluence page URL | JIRA task issues                   |

### Execution Commands

| Command         | Purpose                    | Input                      | Output                  |
| --------------- | -------------------------- | -------------------------- | ----------------------- |
| `/do:task`      | Implement JIRA task        | Issue key (e.g., PROJ-123) | Complete implementation |
| `/do:changelog` | Update changelog           | Version, type, message     | Updated CHANGELOG.md    |
| `/do:commit`    | Create conventional commit | Staged changes             | Git commit              |
| `/do:pr`        | Create pull request        | Current branch             | GitHub PR               |

## Workflow Benefits

1. **Systematic Approach** - Structured methodology from ideation to implementation
2. **Full Traceability** - Every task links back to requirements and features
3. **Quality Assurance** - Built-in validation, testing, and documentation steps
4. **Context Preservation** - All decisions and requirements documented in Confluence
5. **Dependency Management** - Clear task sequencing and critical path identification
6. **Team Collaboration** - JIRA integration enables team visibility and coordination

## Project Structure

```
jira-workflow/
├── .claude/
│   ├── commands/
│   │   ├── do/
│   │   │   ├── task.md          # Execute JIRA task
│   │   │   ├── changelog.md     # Update changelog
│   │   │   ├── commit.md        # Create conventional commit
│   │   │   └── pr.md            # Create pull request
│   │   └── plan/
│   │       ├── brainstorm.md    # Validate ideas
│   │       ├── prd.md           # Create PRD
│   │       ├── feature.md       # Create feature doc
│   │       └── tasks.md         # Break down tasks
│   └── settings.local.json      # Pre-approved permissions
└── README.md
```

## Configuration

### JIRA Project Configuration

The commands automatically detect your JIRA projects and issue types. To customize:

1. Use the Atlassian MCP server's `getVisibleJiraProjects` tool
2. Configure project-specific issue types and workflows
3. Set up custom fields and labels as needed

## Best Practices

1. **Start Small** - Begin with `/plan:brainstorm` to validate ideas before creating features
2. **Keep Tasks Focused** - Use the hierarchical numbering to break down complex work
3. **Follow the Sequence** - Implement tasks in numerical order to respect dependencies
4. **Update JIRA Status** - Let Claude manage status transitions automatically
5. **Review Before PRs** - Use the quality validation steps before creating pull requests
6. **Link Everything** - Maintain links between tasks, features, and PRDs

## Troubleshooting

### Authentication Issues

1. Ensure you've completed the browser authentication flow when prompted
2. Verify you have access to the Atlassian site you're trying to connect to
3. Check that you authorized Claude Code with the necessary permissions
4. Try re-authenticating by running `claude mcp remove atlassian` and then re-adding the server

### Permission Denied Errors

1. Update `.claude/settings.local.json` to pre-approve operations
2. Check your Atlassian user has appropriate JIRA/Confluence permissions
3. Verify OAuth scopes include required permissions

## Contributing

Contributions are welcome! To add new commands:

1. Create a new `.md` file in `.claude/commands/do/` or `.claude/commands/plan/`
2. Follow the existing command structure
3. Document the command in this README
4. Test thoroughly with real JIRA/Confluence instances

## License

MIT License - See LICENSE file for details

## Support

For issues with:

- **Claude Code**: Visit [github.com/anthropics/claude-code/issues](https://github.com/anthropics/claude-code/issues)
- **Atlassian Rovo MCP Server**: Visit [support.atlassian.com/atlassian-rovo-mcp-server](https://support.atlassian.com/atlassian-rovo-mcp-server/)
- **This Workflow System**: Open an issue in this repository

## Acknowledgments

Built with:

- [Claude Code](https://claude.com/claude-code) - Anthropic's CLI for Claude
- [Atlassian Rovo MCP Server](https://support.atlassian.com/atlassian-rovo-mcp-server/) - JIRA/Confluence integration via Atlassian Rovo
- [Model Context Protocol](https://modelcontextprotocol.io) - Tool integration framework
