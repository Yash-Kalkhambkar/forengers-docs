---
title: Deployment & Vercel Integration
description: How deployments work on forengers.in and why we use a local Git email
layout: libdoc_page.liquid
permalink: vercel-deployment.html
tags:
    - deployment
    - vercel
    - git
tocEnabled: false
date: false
eleventyNavigation:
    key: Deployment & Vercel
---

## Table of Contents
1. [Overview](#overview)
2. [How Our Vercel Builds Work](#how-our-vercel-builds-work)
3. [Why We Use a Local Git Email](#why-we-use-a-local-git-email)
4. [Deployment Command](#deployment-command)
---

## Overview

This project deploys using **Vercel’s Git-based workflow**, which automatically builds and deploys the website whenever commits are pushed.  
To ensure error-free and consistent deployments across contributors, we require a specific **local Git configuration** inside this repository.

---

## Why We Use a Local Git Email

To avoid inconsistencies and ensure Vercel recognizes commits correctly, our repo uses a shared local Git email:

```sh
git config --local user.email "forengers.help@gmail.com"
````

This ensures:

* Vercel correctly associates commits with deployments
* Build metadata remains clean and uniform
* No identity or permission mismatches during deployment

This **does not modify your global Git identity** — it applies only to this project.

---

## Deployment Command

Before pushing any code for deployment, run:

```sh
git config --local user.email "forengers.help@gmail.com"
```

Then commit and push normally.
Vercel will automatically trigger the deployment.

---