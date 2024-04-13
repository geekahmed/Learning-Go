# Chapter 01. Data Engineering Described
**Setting Up Your Go Environment**

* **If you've coded in Go, you're mostly set:**  But, consider updating for the latest tools and workflows.
* **New to Go? Installation is easy:**  Go's official documentation has clear instructions.
* **Key Steps:**
    * Install Go itself
    * Verify your setup 
    * Build a simple "Hello World" to test things out
* **Beyond the Basics:** Explore the rich Go tooling ecosystem for more efficient development. 

## Table of Content
* [Installing the Go Tools](#installing-the-go-tools)
* [Your First Go Program](#your-first-go-program)
* [Choose Your Tools](#choose-your-tools)
* [Makefiles](#makefiles)
* [The Go Compatibility Promise](#the-go-compatibility-promise)
* [Staying Up-to-Date](#staying-up-to-date)
* [Exercises](#exercises)
* [Wrapping Up](#wrapping-up)

### Installing the Go Tools
**Installing Go**

* **Official Site:** Get the latest installer from the Go website ([https://go.dev/doc/install](https://go.dev/doc/install))
* **Platform Specific:**  Mac (.pkg), Windows (.msi), Linux/BSD (gzipped TAR) have tailored instructions.
* **Tooling Tip:**  Package managers like Homebrew (Mac) or Chocolatey (Windows) can also install Go.

**Key Points:**

* **Path Matters:** Make sure `/usr/local/go/bin` is in your $PATH so the `go` command works.
* **Native Binaries:** Go programs compile down to a single executable, no extra runtime needed! 

**Verify Your Setup**

* **`go version` check:**  This command should print your installed Go version and system details.

**Troubleshooting**

* **Path Issues:** `which go` on Unix-like systems helps find path problems.
* **Architecture Mismatch:** (Linux/BSD) Ensure you have the right bit version (32/64-bit) and chip architecture.

**Beyond the Basics**

* **Go's Rich Toolset:** `go` is your gateway -- `go build`, `go fmt`, `go mod`, `go test`, etc.
* **Code Organization:** Modern Go gives you freedom. Ignore old advice about `GOPATH`. 

### Your First Go Program
**Your First Go Program**

* **Module Setup:**
    * Create a project directory (e.g., `mkdir ch1`)
    * Initialize a Go module: `go mod init hello_world` 
* **hello.go:**
    * **package main:** Go programs need a `main` package for the entry point.
    * **import "fmt":** Utilize the standard library's formatting package.
    * **func main():** The program's starting point.
    * **fmt.Println("Hello, world!"):** Print your classic greeting.

**Building and Running**

* **`go build`:** Compiles your code into an executable (named after your module).
* **Run:** `./hello_world` (or `./hello_world.exe` on Windows)

**Essential Go Tooling**

* **`go fmt`:**  Enforces Go's standard code formatting. Always run this! 
    * Example: `go fmt ./...` formats your current directory and subdirectories.
* **`go vet`:** Catches common *syntactically valid* coding mistakes.
    * Detects things like missing format string arguments.

**Key Concepts**

* **Semicolon Insertion:** Go adds semicolons for you (mostly). Be mindful of brace placement to avoid unintended consequences. 
* **Code Quality:** `go fmt` and `go vet` are your first line of defense, but consider third-party tools and resources like "Effective Go" for best practices. 

### Choose Your Tools
**Choosing Your Go Development Tools**

**IDEs**

* **Visual Studio Code (Free):**
    * Popular, extensible text editor that becomes a Go IDE with the Go extension.
    * Relies on Marketplace extensions for Go-specific features (Delve debugger, gopls language server).
* **GoLand (Commercial):**
    * JetBrains' dedicated Go IDE, known for excellent refactoring and debugging support.
    * Includes many other tools out of the box (JavaScript, database tools, etc.).
    * Free licenses for qualifying students and open-source contributors.

**Other Options**

* Go support exists for most major text editors and IDEs. Pick what you're comfortable with.

**The Go Playground**

* **Online Environment:**  Web-based for quick code experimentation and sharing. 
* **Features:** 
    * Run your Go code instantly
    * `Format` button for automatic formatting
    * `Share` for creating unique URLs
* **Limitations:**
    * Limited Go versions
    * Restricted network access
    * Not for sensitive code (shared publicly if you use the Share feature) 

### Makefiles
**Automating Your Build with Makefiles**

* **What is make?** A classic tool used since 1976 for specifying build steps and dependencies. It ensures consistent builds across developers and environments.
* **Why use it?** Prevents  "works on my machine" issues by enforcing steps like formatting and code checks before a build. 
* **Key Concepts:**
    * **Targets:** Name of a build step (e.g., `build`, `fmt`, `vet`)
    * **Dependencies:** Targets that *must* run before this one (e.g., `build` depends on `fmt` and `vet` running first)
    * **Tasks:** Indented lines (using tabs!) are the commands for that target.
* **Basic Makefile Example:**
```
.DEFAULT_GOAL := build

.PHONY: fmt vet build

fmt:
    go fmt ./...

vet: fmt
    go vet ./...

build: vet
    go build 
```

**Make in Action**

* `make`:  Runs the default target (`build`) doing formatting, vetting, and then compiling.
* `make vet`:  Runs code checks.
* `make fmt`:  Formats your Go code.

**Caveats**

* **Tabs Matter:** Indentation must use tab characters.
* **Windows:** Install `make` first (e.g., using Chocolatey). 

### The Go Compatibility Promise
**Go's Compatibility Promise**

* **Key Idea:** Go prioritizes stability. Code written for Go 1.x should continue working in future 1.x releases.
* **Scope:** 
    * **Includes:** Go language specification and the standard library 
    * **Excludes:** The `go` command itself (its flags and behavior may change)
* **Exceptions:**  Breaking changes *may* happen, but only for critical bug or security fixes.
* **Why This Matters:** 
    * Reduces upgrade headaches
    * Enables long-term project confidence 

**Reference:**  Russ Cox's GopherCon 2022 talk "Compatibility: How Go Programs Keep Working" goes into further detail. 

### Staying Up-to-Date
**Updating Your Go Environment**

* **Standalone Binaries Rock:** Go programs don't rely on a runtime, so you can mix versions on the same machine without worry. 
* **Updating Methods:**
    * **Mac/Windows (Installers):** Download the latest installer from [https://golang.org/dl](https://golang.org/dl). It handles replacing the old version.
    * **Mac (Homebrew):** `brew upgrade go`
    * **Windows (Chocolatey):** `choco upgrade golang`
    * **Linux/BSD:**
        1. Download the latest version 
        2. Backup your existing `/usr/local/go` (just in case)
        3.  Untar the new version into `/usr/local/go`
        4.  Clean up the old backup

> **Tip:**  Updating your Go tools won't break existing deployed programs. 

### Exercises
> 1. Take the “Hello, world!” program and run it on The Go Playground. Share a link to the code in the playground with a coworker who would love to learn about Go.

**Answer**: https://go.dev/play/p/z4CNGo3QAtL 

> 2. Add a target to the Makefile called clean that removes the hello_world binary and any other temporary files created by go build. Take a look at the Go command documentation to find a go command to help implement this.

**Answer**:

```
.DEFAULT_GOAL := build

.PHONY: fmt vet build

fmt:
    go fmt ./...

vet: fmt
    go vet ./...

build: vet
    go build 

clean: build
    go clean
```

> 3. Experiment with modifying the formatting in the “Hello, world!” program. Add blank lines, spaces, change indentation, insert newlines. After making a modification, run go fmt to see if the formatting change is undone. Also, run go build to see if the code still compiles. You can also add additional fmt.Println calls so you can see what happens if you put blank lines in the middle of a function.


### Wrapping Up
**Chapter 1 Wrap-Up**

* **You've Got This:** Your Go development environment is set up and ready to go.
* **Key Tools:**
    * Text editor or IDE with Go extensions (VS Code, GoLand, etc.)
    * The `go` command for building, formatting (`go fmt`), and quality checks (`go vet`)
    * Consider using Makefiles for automating your build process
* **Go's Promise:**  Stability is a priority. Your code should work across Go 1.x releases.
 
**Next Up: Chapter 2**

Get ready to dive into Go's built-in types and how to work with variables. 
