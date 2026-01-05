# NPM and Package Management

## Table of Contents
1. [Introduction](#1-introduction)
2. [NPM Basics](#2-npm-basics)
3. [Package.json](#3-packagejson)
4. [Installing Packages](#4-installing-packages)
5. [Global vs Local Installation](#5-global-vs-local-installation)
6. [Common NPM Commands](#6-common-npm-commands)
7. [Quick Reference](#7-quick-reference)
8. [Interview Questions](#8-interview-questions)

---

## 1. Introduction

### 1.1 What is NPM?
**NPM** (Node Package Manager) is the default package manager for Node.js. It provides:
- Online repository for packages at [npmjs.org](https://npmjs.org)
- Command-line utility for package management

### 1.2 Key Features
- Install packages/modules
- Version management
- Dependency management
- Script running
- Package publishing

### 1.3 Checking NPM Version

```bash
$ npm --version
9.6.7
```

---

## 2. NPM Basics

### 2.1 Initializing a Project

```bash
$ npm init
```

Interactive prompts:
- Package name
- Version
- Description
- Entry point
- Test command
- Git repository
- Keywords
- Author
- License

**Quick initialization:**
```bash
$ npm init -y
```

### 2.2 Installing a Package

```bash
$ npm install <package-name>
```

Example:
```bash
$ npm install express
```

### 2.3 Package Installation Location

```
project-folder/
├── node_modules/
│   ├── express/
│   └── (other dependencies)
├── package.json
└── package-lock.json
```

---

## 3. Package.json

### 3.1 What is package.json?
A plain JSON file containing metadata about the Node.js project:
- Project name and version
- Dependencies
- Scripts
- Author information

### 3.2 Sample package.json

```json
{
  "name": "my-app",
  "version": "1.0.0",
  "description": "My Node.js application",
  "main": "index.js",
  "scripts": {
    "start": "node index.js",
    "test": "jest",
    "dev": "nodemon index.js"
  },
  "keywords": ["nodejs", "express"],
  "author": "Developer Name",
  "license": "MIT",
  "dependencies": {
    "express": "^4.18.2",
    "mongoose": "^7.0.0"
  },
  "devDependencies": {
    "nodemon": "^2.0.22",
    "jest": "^29.5.0"
  }
}
```

### 3.3 Key Fields

| Field | Description |
|-------|-------------|
| `name` | Package name |
| `version` | Semantic version |
| `main` | Entry point file |
| `scripts` | NPM scripts |
| `dependencies` | Production dependencies |
| `devDependencies` | Development dependencies |

### 3.4 Version Numbers

```
^4.18.2
│ │  │
│ │  └── Patch (bug fixes)
│ └───── Minor (new features, backward compatible)
└─────── Major (breaking changes)

^ = Compatible with version (minor updates allowed)
~ = Approximately equivalent (patch updates only)
```

---

## 4. Installing Packages

### 4.1 Production Dependencies

```bash
# Install and save to dependencies
$ npm install express

# Explicit save (default in npm 5+)
$ npm install express --save
```

### 4.2 Development Dependencies

```bash
# Install as dev dependency
$ npm install nodemon --save-dev
$ npm install nodemon -D
```

### 4.3 Installing All Dependencies

```bash
# Install all from package.json
$ npm install
```

### 4.4 Installing Specific Version

```bash
$ npm install express@4.17.1
```

---

## 5. Global vs Local Installation

### 5.1 Local Installation (Default)

```bash
$ npm install express
```

- Installed in `./node_modules`
- Available only in project
- Accessible via `require()`

### 5.2 Global Installation

```bash
$ npm install -g express
```

- Installed in system directory
- Available as CLI commands
- Cannot use `require()` directly

### 5.3 Comparison

| Feature | Local | Global |
|---------|-------|--------|
| Location | `./node_modules` | System directory |
| Access | `require()` | CLI only |
| Project-specific | Yes | No |
| Command | `npm install pkg` | `npm install -g pkg` |

### 5.4 Common Global Packages

```bash
# Development tools
$ npm install -g nodemon
$ npm install -g typescript
$ npm install -g create-react-app

# Utility tools
$ npm install -g npm-check-updates
$ npm install -g http-server
```

---

## 6. Common NPM Commands

### 6.1 Package Management

| Command | Description |
|---------|-------------|
| `npm install` | Install all dependencies |
| `npm install <pkg>` | Install package |
| `npm install <pkg> -g` | Install globally |
| `npm install <pkg> -D` | Install as dev dependency |
| `npm uninstall <pkg>` | Remove package |
| `npm update` | Update all packages |
| `npm update <pkg>` | Update specific package |

### 6.2 Project Commands

| Command | Description |
|---------|-------------|
| `npm init` | Create package.json |
| `npm init -y` | Create with defaults |
| `npm run <script>` | Run npm script |
| `npm start` | Run start script |
| `npm test` | Run test script |

### 6.3 Information Commands

| Command | Description |
|---------|-------------|
| `npm list` | List installed packages |
| `npm list -g` | List global packages |
| `npm outdated` | Check outdated packages |
| `npm view <pkg>` | View package info |
| `npm search <term>` | Search packages |

---

## 7. Quick Reference

### 7.1 Essential Commands

```bash
# Initialize project
npm init -y

# Install dependencies
npm install

# Add package
npm install express

# Add dev package
npm install -D nodemon

# Run scripts
npm start
npm test
npm run dev

# Update packages
npm update
```

### 7.2 Package.json Scripts

```json
{
  "scripts": {
    "start": "node server.js",
    "dev": "nodemon server.js",
    "build": "webpack --mode production",
    "test": "jest --coverage"
  }
}
```

### 7.3 NPM vs NPX

| NPM | NPX |
|-----|-----|
| Package manager | Package runner |
| Installs packages | Runs packages directly |
| `npm install pkg` | `npx pkg` |

---

## 8. Interview Questions

### Q1: What is NPM?
**Answer**: NPM (Node Package Manager) is the default package manager for Node.js. It provides an online repository for packages and a CLI utility for installing, managing, and publishing packages.

### Q2: What is package.json?
**Answer**: package.json is a JSON file containing metadata about the Node.js project including name, version, dependencies, scripts, and other configuration. NPM uses it to manage project dependencies.

### Q3: What is the difference between dependencies and devDependencies?
**Answer**:
- **dependencies**: Required for production (express, mongoose)
- **devDependencies**: Required only for development (nodemon, jest)

### Q4: What is the difference between local and global installation?
**Answer**:
- **Local**: Installed in `node_modules`, project-specific, accessible via `require()`
- **Global**: Installed system-wide, used for CLI tools, cannot use `require()`

### Q5: What does `npm install` do without arguments?
**Answer**: It reads package.json and installs all packages listed in dependencies and devDependencies.

### Q6: What is package-lock.json?
**Answer**: It locks the exact versions of all dependencies (including nested dependencies) to ensure consistent installs across different machines and environments.

---

## Navigation

← Previous: [30_NodeJS_Introduction.md](./30_NodeJS_Introduction.md) | Next: [32_Modules_and_Exports.md](./32_Modules_and_Exports.md) →

---

*Source: CDAC PG-DAC Web Programming Technologies Course - Day 07*
