# FluxCD and Flagger Demo - Cloud Native Days Italy 2025

This repository demonstrates advanced deployment strategies using FluxCD and Flagger for the Cloud Native Days Italy 2025 conference.

> Warning: everything in here was written by Claude and fixed by me (it works, but it ain't pretty )

## Overview

This demo showcases:
- GitOps workflows with FluxCD
- Progressive delivery with Flagger
- Canary deployments and automated rollbacks
- Modern cloud-native deployment patterns

## Prerequisites

### Installing Devbox

Devbox provides isolated, reproducible development environments. Install it using one of the following methods:

#### macOS/Linux (Homebrew)
```bash
brew install jetpack-io/devbox/devbox
```

#### Linux/macOS (curl)
```bash
curl -fsSL https://get.jetpack.io/devbox | bash
```

#### Windows (PowerShell)
```powershell
iwr -useb https://get.jetpack.io/devbox | iex
```

For more installation options, visit: https://www.jetpack.io/devbox/docs/installing_devbox/

## Getting Started

1. Clone this repository
2. Install devbox (see above)
3. Initialize the development environment:
   ```bash
   devbox shell
   ```
4. Run tasks using go-task:
   ```bash
   task --list
   ```

## Development Environment

This project uses devbox to manage development dependencies. All required tools are automatically installed when you enter the devbox shell.


### CI/CD Pipeline
The GitHub Actions workflow automatically builds and pushes both image variants to the GitHub Container Registry when changes are pushed to the main branch.

## OCI Registry Authentication

### Create the GitHub Container Registry Secret

The OCI secret is required for FluxCD to authenticate with the GitHub Container Registry when pulling oci images used in this demo (note the registry is public so in this case you would not even need the secret):

```bash
flux create secret oci ghcr-auth \
  --namespace flux-system \
  --url=ghcr.io \
  --username=YOUR_GITHUB_USERNAME \
  --password=$GITHUB_TOKEN
```

**Prerequisites:**
- Set your `GITHUB_TOKEN` environment variable with a personal access token that has `packages:read` permissions
- Replace `YOUR_GITHUB_USERNAME` with your actual GitHub username

## MCP Server

  "flux-operator-mcp": {
     "command": "/usr/local/bin/flux-operator-mcp",
     "args": ["serve"],
     "env": {
       "KUBECONFIG": "/home/ric/.kube/config"
     }
   }