---
title: Using pnpm in Our Project
description: Why we use pnpm, how it works, and essential commands for contributors
layout: libdoc_page.liquid
permalink: pnpm.html
tags:
    - pnpm
    - package-manager
    - tooling
tocEnabled: false
date: false
eleventyNavigation:
    key: pnpm
---

## Table of Contents
1. [Why We Use pnpm](#why-we-use-pnpm)
2. [How pnpm Works](#how-pnpm-works)
3. [Essential Commands](#essential-commands)
---

## Why We Use pnpm

Our project uses **pnpm** as the primary package manager because it is faster, more efficient, and more reliable for large-scale or multi-contributor projects compared to npm or yarn.

### Key Benefits

- **🚀 Faster installs**  
  pnpm uses a content-addressable storage system, making dependency installs significantly faster.

- **📦 Less disk usage**  
  Dependencies are stored *once* on your machine and hard-linked across projects, saving gigabytes of space.

- **🔒 Strict dependency isolation**  
  pnpm ensures packages cannot access undeclared dependencies, leading to fewer “it works on my machine” issues.

- **⚙️ Production-ready workflows**  
  pnpm supports workspace features, monorepos, and efficient CI/CD workflows out of the box.

These advantages make pnpm ideal for consistent builds and stable development across all contributors.

---

## How pnpm Works

Unlike npm and yarn, which duplicate all dependency files inside each project’s `node_modules`, **pnpm creates a global content-addressable store** on your machine.

1. When you install a package, pnpm stores it in a **global store** (e.g., `~/.pnpm-store`).
2. Your project’s `node_modules` folder doesn’t contain full copies—it contains **symlinks or hard links** to that global store.
3. This means:
   - Dependencies are not duplicated across repos  
   - Corrupted installs are rare  
   - Installations become nearly instant after the first time  

Because pnpm links dependencies instead of copying them, the structure is strict and predictable. This prevents accidental access to undeclared dependencies, improving project stability.

---

## Essential Commands

Below are the core pnpm commands every team member should know.

### Install dependencies

```sh
pnpm install
````

Installs all project dependencies based on the `pnpm-lock.yaml`.

---

### Add a dependency

```sh
pnpm add <package-name>
```

Add a package to `dependencies`.

---

### Add a dev dependency

```sh
pnpm add -D <package-name>
```

---

### Remove a dependency

```sh
pnpm remove <package-name>
```

---

### Update dependencies

```sh
pnpm update
```

---

### Run a script (similar to npm run)

```sh
pnpm run <script-name>
```

Example:

```sh
pnpm run dev
```

---

### Execute a package binary

```sh
pnpm exec <command>
```

Example:

```sh
pnpm exec astro build
```

---

### Install a package globally (rarely needed)

```sh
pnpm add -g <package>
```

---

## Summary for Team Members

* Always use **pnpm** instead of npm/yarn for installations and scripts.
* This ensures:
  ✔ faster installs
  ✔ less disk usage
  ✔ more consistent builds across contributors