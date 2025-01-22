# Setting up a dev container for Go

* Primary author: [Mason Drabik](https://github.com/mkdrabik)

* Reviewer: [Riley Warmuth](https://github.com/rileywar)


Install Docker:

Download and install Docker Desktop from Docker's website.
Ensure Docker is running and the Docker CLI works on your system.
Install VS Code:

Download and install Visual Studio Code from VS Code's website.
Install the Remote - Containers Extension:

In VS Code, go to the Extensions Marketplace (Ctrl+Shift+X or Cmd+Shift+X on Mac).
Search for Dev Containers and install the official "Remote - Containers" extension.


Create a folder for your project
mkdir go-dev-container && cd go-dev-container


Inside your project folder, create a .devcontainer directory:
mkdir .devcontainer

Create a devcontainer.json file in the .devcontainer folder:
touch .devcontainer/devcontainer.json
Add the following configuration to the devcontainer.json file:

json
Copy
Edit
{
  "name": "Go Dev Container",
  "image": "golang:1.20",
  "features": {
    "ghcr.io/devcontainers/features/go:1": {
      "version": "1.20"
    }
  },
  "customizations": {
    "vscode": {
      "settings": {
        "go.toolsManagement.autoUpdate": true,
        "go.useLanguageServer": true,
        "editor.formatOnSave": true
      },
      "extensions": [
        "golang.Go"
      ]
    }
  },
  "mounts": [
    "source=/var/run/docker.sock,target=/var/run/docker.sock,type=bind"
  ],
  "postCreateCommand": "go mod tidy",
  "remoteUser": "root"
}
Step 4: (Optional) Add Dockerfile
If you need to customize the base image, create a Dockerfile in the .devcontainer folder:

# Install additional tools if needed
RUN apt-get update && apt-get install -y curl git && rm -rf /var/lib/apt/lists/*
Update the devcontainer.json to use the Dockerfile:
{
  "name": "Go Dev Container",
  "build": {
    "dockerfile": "Dockerfile"
  },
  "customizations": {
    "vscode": {
      "extensions": ["golang.Go"]
    }
  },
  "postCreateCommand": "go mod tidy",
  "remoteUser": "root"
}

Step 5: Open the Project in the Dev Container
Open your project in VS Code.
Press F1 or Ctrl+Shift+P and type "Dev Containers: Reopen in Container".
VS Code will build the container, set up the environment, and reopen your project inside the container.

Step 6: Verify the Setup
Open a terminal in VS Code (`Ctrl+``).

Check the Go version:
go version
Run your Go code to ensure everything works.
