---
title: Getting Started with Rill Developer
description: A comprehensive guide to installing and using Rill Developer for new users
---

# Getting Started with Rill Developer

Welcome to Rill Developer! This guide will walk you through the process of installing, configuring, and running your first Rill project. Rill Developer is a powerful tool that makes it effortless to transform your datasets using SQL.

## System Requirements

Before you begin, make sure your system meets the following requirements:

- NodeJS version 16 or higher
- For Ubuntu users: `g++` compiler (required for compiling DuckDB)

## Installation

To install Rill Developer, follow these steps:

1. Open your terminal or command prompt.

2. Install Rill Developer globally using npm:

```bash
npm install -g @rilldata/rill
```

Note: This installation process involves compiling DuckDB, which may take several minutes to complete. Please be patient during the installation.

## Creating Your First Rill Project

Now that you have Rill Developer installed, let's create your first project:

1. Initialize a new Rill project:

```bash
rill init
```

This command will create a new Rill project in your current directory.

2. Import your data sources. Rill Developer supports .parquet, .csv, and .tsv files:

```bash
rill import-source /path/to/your/data.parquet
rill import-source /path/to/your/data.csv
rill import-source /path/to/your/data.tsv
```

3. Start the Rill Developer User Interface:

```bash
rill start
```

The Rill Developer UI will be available at http://localhost:8080.

## Quick Start Example

If you want to quickly explore Rill Developer's capabilities, you can use the built-in example project:

```bash
rill initialize-example-project
```

This command will set up a project using an OpenSky Network dataset and launch the Rill Developer UI.

## Basic Configuration

Here are some helpful configuration options to customize your Rill Developer experience:

- Specify a project directory:
  ```bash
  rill init --project /path/to/your/project
  ```

- Name your data source:
  ```bash
  rill import-source /path/to/data.parquet --name my_custom_source_name
  ```

- Use a custom delimiter for text files:
  ```bash
  rill import-source /path/to/data.txt --delimiter "|"
  ```

- Connect to an existing DuckDB database:
  ```bash
  rill init --db /path/to/duckdb/file
  ```

## Next Steps

Now that you have Rill Developer up and running, you can start exploring your data and creating SQL transformations. Here are some suggestions for what to do next:

1. Explore the Rill Developer UI to familiarize yourself with the interface.
2. Try writing some SQL queries to analyze your imported data.
3. Experiment with different data transformations and visualizations.
4. Check out the [Rill Developer SQL Dialect](https://duckdb.org/docs/sql/introduction) documentation to learn more about the supported SQL features.

## Troubleshooting

If you encounter any issues during installation or while using Rill Developer, consider the following:

- Ensure you have the latest version of Rill Developer installed:
  ```bash
  npm install -g @rilldata/rill
  ```

- If you see a 404 error when accessing the UI, wait a few more minutes as the build process might still be ongoing.

- For more detailed help, use the built-in help command:
  ```bash
  rill --help
  ```

If you continue to experience problems, don't hesitate to [file an issue](https://github.com/rilldata/rill-developer/issues/new/choose) on the Rill Developer GitHub repository or reach out to the community on the [Rill Discord](https://bit.ly/3unvA05) channel.

Happy data analyzing with Rill Developer!