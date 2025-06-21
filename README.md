# FluxCD and Flagger Demo - Cloud Native Days Italy 2025

This repository demonstrates advanced deployment strategies using FluxCD and Flagger for the Cloud Native Days Italy 2025 conference.

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

## Create the secret
flux create secret oci flux-system \
  --namespace flux-system \
  --url=ghcr.io \
  --username=ricCap \
  --password=$GITHUB_TOKEN



  "flux-operator-mcp": {
     "command": "/usr/local/bin/flux-operator-mcp",
     "args": ["serve"],
     "env": {
       "KUBECONFIG": "/home/ric/.kube/config"
     }
   }