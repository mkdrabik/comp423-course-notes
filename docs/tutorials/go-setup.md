# Setting up a dev container for Go

* Primary author: [Mason Drabik](https://github.com/mkdrabik)

* Reviewer: [Riley Warmuth](https://github.com/rileywar)
#
# Prerequsites 

**Install Docker:** Download and install Docker Desktop from Docker's website. [Get Docker Here](https://www.docker.com/products/docker-desktop)

**Install VS Code:** Download and install VS Code from VS Code's website. [Get VS Code Here](https://code.visualstudio.com/)

**Install the Remote - Containers Extension:** In VS Code, go to the Extensions Marketplace (Ctrl+Shift+X or Cmd+Shift+X on Mac).
Search for Dev Containers and install the official "Remote - Containers" extension. 
# 

# Part 1: Setting up your Environment
**1.Create a folder for your project:**
Open a new window in VS Code, then open a new terminal and run the following commands.
```bash
mkdir go-dev-container 
cd go-dev-container
```
This will create a folder for your project and set your current working directory to that folder. ```Mkdir``` creates the directory and ```cd``` moves you to that folder. 

**2. Create a folder for your devcontainer:**
Open your project in VS Code by using Crtl+O (on mac Cmd+O) and then finding your project. 
Once inside your project folder, create a .devcontainer directory: ```mkdir .devcontainer```


**3. Create a devcontainer.json file in the .devcontainer folder:**
```bash
touch .devcontainer/devcontainer.json
```
This creates the file devcontainer.json in the .devconatiner directory.

**4.Add the following configuration to the devcontainer.json file:**

```json
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
```

**Step 5: Open the Project in the Dev Container:**
Press Ctrl+Shift+P (on mac Cmd+Shift+P) and type "Dev Containers: Reopen in Container".
VS Code will then build the container, set up the environment, and reopen your project inside the container.

**Step 6: Verify the Setup:**
Open a terminal in VS Code and check the Go version.
```bash
go version
```

If your output looks something like this, everything is properly set up and you can now move on to writing your program!
```bash
go version go1.20.14 linux/arm64
```
#
#
# Part 2: Running Go

We are now going to run a simple go program in your container.

**Step 1: Create a Go file.**
This can be done manually in VS Code or use the following command in your directory called "go-dev-container" (or whatever your main directory was called). 

```bash
touch main.go
```

**Step 2: Edit your file.**
Open main.go in VS Code and add the following. 

```go
package main

import "fmt"

func main() {
    fmt.Println("Hello COMP423")
}
```

!!! question "Why do we need package main and import "fmt"?"

    In Go, source files are organized into system directories called packages. These packages are a way to group functions and contain all files in the same directory. The main function in the main package is the starting point of our program. We imported the popular "fmt" package which contains functions for formatting text, including printing to the console. This package is one of the standard library packages that were installed when Go was installed. We are not limited to importing just "fmt" to import another package simply add ```import <package name>``` below previous imports.


**Step 3: Run your program.**


!!! note " Running a program in Go "

    In Go, there are two different ways to run your program ```go run``` and ```go build```. The difference between the two is that ```go run``` compiles your code into a temporary executable which it then runs and deletes after it is done executing. This is ideal for quick testing. However, ```go build``` creates an executable binary file of your code, which is then saved to your current directory. You can then run by typing ```./<name of file>``` in the terminal. Using this command is more ideal for producing binaries for later use or distribution. 


**Go run:**
To run your program type the following into your terminal. This should print "Hello COMP 423" to your terminal.

```go 
go run main.go
```
#
**Go build:**
In order to run ```go build``` we must first add a new file to our directory. 

```go
go mod init my-go-project
```
This creates a go.mod file which manages the dependencies you are using. To to add module requirements and sums use ```go tidy```. Now that we have created a go.mod file you can run ```go build``` then run your executable file. 

```go 
go build main.go
./main.go
```

"Hello COMP423" should be printed as a result. Congratulations you have just set up a dev container for Go and executed a program with it!

