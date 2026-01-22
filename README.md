# clean-claude

Meta repo for running Claude Code in isolated Docker containers using GitHub Codespaces.

## Features

- **GitHub Codespaces**: Cloud development environment with Docker-in-Docker
- **Ephemeral containers**: Safe sandbox environments, destroy/recreate anytime
- **Persistent code**: All projects committed to this repo
- **Pre-configured**: Node.js, Python, VS Code CLI, Claude Code ready to go
- **Minimal friction**: Two simple commands to create and run projects

## Quick Start

### 1. Open in Codespaces

Click the green "Code" button on GitHub and select "Create codespace on main" (or your branch).

The Codespace will automatically set up with Docker and Claude CLI installed.

### 2. Create a new project

```bash
./scripts/new my-app
```

This will:
1. Create `projects/my-app/` directory
2. Build the Docker image (first time only)
3. Start a container with the project mounted

### 3. Work on an existing project

```bash
./scripts/run my-app
```

### 4. Run Claude Code

You can use Claude Code in two ways:

**From the Codespace (host):**
```bash
claude
```

**Inside an ephemeral container:**
```bash
docker exec -it clean-claude-my-app claude
```

Or enter the container first:
```bash
docker exec -it clean-claude-my-app bash
claude
```

### 5. Destroy a container (code is safe!)

```bash
docker rm -f clean-claude-my-app
```

Your code in `projects/my-app/` persists in the Codespace.

## Workflow

1. Open repo in Codespaces
2. Create project: `./scripts/new experiment-1`
3. Enter container: `docker exec -it clean-claude-experiment-1 bash`
4. Let Claude build: `claude`
5. Commit when ready: `git add projects/experiment-1 && git commit`
6. Destroy container: `docker rm -f clean-claude-experiment-1`

## Structure

```
clean-claude/
├── projects/          # Your projects (committed to git)
│   ├── my-app/
│   └── experiment-1/
├── docker/
│   └── Dockerfile    # Dev environment definition
├── scripts/
│   ├── new           # Create new project
│   └── run           # Run existing project
└── README.md
```
