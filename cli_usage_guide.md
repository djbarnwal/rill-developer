# Rill CLI Usage Guide

This guide provides comprehensive information on using the Rill Command Line Interface (CLI), including available commands, their options, and example usage. It also offers tips for effectively using the CLI for common tasks and troubleshooting.

## Table of Contents

1. [Installation](#installation)
2. [Getting Started](#getting-started)
3. [Available Commands](#available-commands)
4. [Common Tasks](#common-tasks)
5. [Troubleshooting](#troubleshooting)

## Installation

To install the Rill CLI, follow these steps:

1. [Download the latest release](#) for your operating system.
2. Extract the downloaded archive.
3. Add the extracted directory to your system's PATH.

Verify the installation by running:

```bash
rill version
```

## Getting Started

To begin using the Rill CLI, open your terminal and type `rill` followed by a command. For example:

```bash
rill help
```

This will display a list of available commands and their brief descriptions.

## Available Commands

The Rill CLI offers the following main commands:

1. `rill init`: Initialize a new Rill project
2. `rill build`: Build your Rill project
3. `rill run`: Run your Rill project locally
4. `rill deploy`: Deploy your Rill project
5. `rill logs`: View logs for your deployed project

### rill init

Use this command to create a new Rill project:

```bash
rill init [project-name]
```

Options:
- `--template <template-name>`: Specify a project template to use

### rill build

Build your Rill project:

```bash
rill build
```

Options:
- `--output <directory>`: Specify the output directory for built files

### rill run

Run your Rill project locally:

```bash
rill run
```

Options:
- `--port <port-number>`: Specify the port to run the local server on (default: 3000)

### rill deploy

Deploy your Rill project:

```bash
rill deploy
```

Options:
- `--environment <env-name>`: Specify the deployment environment (e.g., production, staging)

### rill logs

View logs for your deployed project:

```bash
rill logs
```

Options:
- `--tail`: Continuously stream new log entries
- `--since <time>`: Show logs since a specific time (e.g., 1h, 2d)

## Common Tasks

### Creating and Deploying a New Project

1. Initialize a new project:
   ```bash
   rill init my-new-project
   cd my-new-project
   ```

2. Build the project:
   ```bash
   rill build
   ```

3. Test locally:
   ```bash
   rill run
   ```

4. Deploy to production:
   ```bash
   rill deploy --environment production
   ```

### Updating an Existing Project

1. Make changes to your project files
2. Rebuild the project:
   ```bash
   rill build
   ```

3. Test locally:
   ```bash
   rill run
   ```

4. Deploy the updated version:
   ```bash
   rill deploy
   ```

## Troubleshooting

### Common Issues and Solutions

1. **Command not found**: Ensure that the Rill CLI is properly installed and added to your system's PATH.

2. **Build failures**: Check your project for syntax errors or missing dependencies. Use `rill build --verbose` for more detailed error messages.

3. **Deployment issues**: Verify your authentication credentials and network connectivity. Use `rill deploy --debug` for additional information.

4. **Performance problems**: Monitor your application's performance using `rill logs` and consider optimizing your code or scaling your resources.

For more help, consult the [Rill documentation](#) or reach out to the [Rill community forum](#).