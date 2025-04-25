# MCP Git Repo Browser (Node.js)

A Node.js implementation of a Git repository browser using the Model Context Protocol (MCP).

[![GitHub Repository](https://img.shields.io/badge/GitHub-Repository-blue.svg)](https://github.com/bsreeram08/git-commands-mcp)
[![npm package](https://img.shields.io/npm/v/git-commands-mcp.svg)](https://www.npmjs.com/package/git-commands-mcp)

## Installation

### Installing via Smithery

To install Git Repository Browser for Claude Desktop automatically via [Smithery](https://smithery.ai/server/@bsreeram08/git-commands-mcp):

```bash
npx -y @smithery/cli install @bsreeram08/git-commands-mcp --client claude
```

### NPM (Recommended)

```bash
npm install -g git-commands-mcp
```

### Manual Installation

```bash
git clone https://github.com/bsreeram08/git-commands-mcp.git
cd git-commands-mcp
npm install
```

## Configuration

Add this to your MCP settings configuration file:

```json
{
  "mcpServers": {
    "git-commands-mcp": {
      "command": "git-commands-mcp"
    }
  }
}
```

For manual installation, use:

```json
{
  "mcpServers": {
    "git-commands-mcp": {
      "command": "node",
      "args": ["/path/to/git-commands-mcp/src/index.js"]
    }
  }
}
```

## Features

The server provides the following tools:

### Basic Repository Operations

1. `git_directory_structure`: Returns a tree-like representation of a repository's directory structure

   - Input: Repository URL
   - Output: ASCII tree representation of the repository structure

2. `git_read_files`: Reads and returns the contents of specified files in a repository

   - Input: Repository URL and list of file paths
   - Output: Dictionary mapping file paths to their contents

3. `git_search_code`: Searches for patterns in repository code
   - Input: Repository URL, search pattern, optional file patterns, case sensitivity, and context lines
   - Output: JSON with search results including matching lines and context

### Branch Operations

4. `git_branch_diff`: Compare two branches and show files changed between them
   - Input: Repository URL, source branch, target branch, and optional show_patch flag
   - Output: JSON with commit count and diff summary

### Commit Operations

5. `git_commit_history`: Get commit history for a branch with optional filtering

   - Input: Repository URL, branch name, max count, author filter, since date, until date, and message grep
   - Output: JSON with commit details

6. `git_commits_details`: Get detailed information about commits including full messages and diffs

   - Input: Repository URL, branch name, max count, include_diff flag, author filter, since date, until date, and message grep
   - Output: JSON with detailed commit information

7. `git_local_changes`: Get uncommitted changes in the working directory
   - Input: Local repository path
   - Output: JSON with status information and diffs

## Project Structure

```
git-commands-mcp/
├── src/
│   ├── index.js         # Entry point
│   ├── server.js        # Main server implementation
│   ├── handlers/        # Tool handlers
│   │   └── index.js     # Tool implementation functions
│   └── utils/           # Utility functions
│       └── git.js       # Git-related helper functions
├── package.json
└── readme.md
```

## Implementation Details

- Uses Node.js native modules (crypto, path, os) for core functionality
- Leverages fs-extra for enhanced file operations
- Uses simple-git for Git repository operations
- Implements clean error handling and resource cleanup
- Creates deterministic temporary directories based on repository URL hashes
- Reuses cloned repositories when possible for efficiency
- Modular code structure for better maintainability

## Requirements

- Node.js 14.x or higher
- Git installed on the system

## Usage

If installed globally via npm:

```bash
git-commands-mcp
```

If installed manually:

```bash
node src/index.js
```

The server runs on stdio, making it compatible with MCP clients.

## CI/CD

This project uses GitHub Actions for continuous integration and deployment:

### Automatic NPM Publishing

The repository is configured with a GitHub Actions workflow that automatically publishes the package to npm when changes are pushed to the master branch.

#### Setting up NPM_AUTOMATION_TOKEN

To enable automatic publishing, you need to add an npm Automation token as a GitHub secret (this works even with accounts that have 2FA enabled):

1. Generate an npm Automation token:

   - Log in to your npm account on [npmjs.com](https://www.npmjs.com/)
   - Go to your profile settings
   - Select "Access Tokens"
   - Click "Generate New Token"
   - Select "Automation" token type
   - Set the appropriate permissions (needs "Read and write" for packages)
   - Copy the generated token

2. Add the token to your GitHub repository:
   - Go to your GitHub repository
   - Navigate to "Settings" > "Secrets and variables" > "Actions"
   - Click "New repository secret"
   - Name: `NPM_AUTOMATION_TOKEN`
   - Value: Paste your npm Automation token
   - Click "Add secret"

Once configured, any push to the master branch will trigger the workflow to publish the package to npm.

## License

MIT License - see the [LICENSE](LICENSE) file for details.

## Links

- [GitHub Repository](https://github.com/bsreeram08/git-commands-mcp)
- [NPM Package](https://www.npmjs.com/package/git-commands-mcp)
- [Report Issues](https://github.com/bsreeram08/git-commands-mcp/issues)
