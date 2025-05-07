# Reference Configurations for Claude Desktop MCP
## Connecting Claude Desktop to Jetbrains on Windows Host with node installed in Windows 
```json
  "jetbrains": {
      "env": {
          "IDE_PORT": "58682"
      },
      "command": "npx",
      "args": [
          "-y",
          "@jetbrains/mcp-proxy"
      ]
  },
```
1. Install MCP Server plugin first
2. Go to Settings -> Debugger -> Allow External Connections
3. Update the port to match the config.  Note, Jetbrains changes ports every launch (it seems).  Editing the Claude config to update the port requires the desktop app to be exited and reopened.  Jetbrains IDE's don't, so I usually  update Jetbrains to match the Claude config instead of vice versa.

## Connecting Claude (in Windows Host) to a dockerized MCP Server (running in Windows Host)

```json
    "github": {
        "command": "docker",
        "args": [
            "run",
            "-i",
            "--rm",
            "-e",
            "GITHUB_PERSONAL_ACCESS_TOKEN",
            "ghcr.io/github/github-mcp-server"
        ],
        "env": {
            "GITHUB_PERSONAL_ACCESS_TOKEN": "<<YOUR TOKEN>>"
        }
```

## Connecting Claude Desktop (in Windows Host) to dockerized MCP Server (running in WSL)

```json
    "filesystem": {
        "command": "wsl.exe",
        "args": [
            "docker",
            "run",
            "-i",
            "--rm",
            "--mount",
            "type=bind,src=<<desired directory>>,dst=/projects",
            "mcp/filesystem",
            "/projects"
        ]
    }
```
## Connecting Claude Desktop (in Windows Host) to uvx packaged MCP Server (running in WSL)
```json
    "git": {
        "command": "wsl.exe",
        "args": [
            "bash",
            "-c",
            "<<full path to uvx>> mcp-server-git --repository <<path to your repo>>"
        ]
    },
