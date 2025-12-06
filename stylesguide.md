---
title: Using Custom Tailwind Colors and Variables
description: How Forengers defines, organizes, and uses custom Tailwind CSS variables such as forengers-dark-green and forengers-light-green.
layout: libdoc_page.liquid
permalink: tailwind-colors.html
tags:
    - tailwind
    - styling
    - css 
tocEnabled: false
date: false
eleventyNavigation:
    key: tailwind-colors
---

## Table of Contents
1. [Why We Use Custom Tailwind Variables](#why-we-use-custom-tailwind-variables)
2. [Where Our Colors Are Defined](#where-our-colors-are-defined)
3. [Available Forengers Brand Colors](#available-forengers-brand-colors)
4. [How to Use These Colors in Components](#how-to-use-these-colors-in-components)
5. [Best Practices for Contributors](#best-practices-for-contributors)

---

## Why We Use Custom Tailwind Variables

Our project includes a **brand-specific design system**, and Tailwind's built-in palette cannot represent our visual identity.  
To ensure consistency across every page, we define a dedicated set of **CSS variables** and reference them inside Tailwind classes.

### Benefits of custom variables

- **🎨 Consistent Branding**  
  Colors like `forengers-dark-green` appear across buttons, headings, sections, navbars, etc.

- **🛠 Easy to update**  
  Changing a value in one place updates the entire website’s theme.

- **🌙 Supports dark mode automatically**  
  Colors can switch based on the theme (`:root` vs `.dark`).

- **📦 Cleaner component code**  
  Components rely on semantic names like `text-forengers-dark-green` instead of hex values.

---

## Where Our Colors Are Defined

All custom Tailwind color variables are defined inside:

```
/src/styles/globals.css
```

These variables are registered under the `@theme` block as:

```css
--color-forengers-light-green: #347c05;
--color-forengers-dark-green: #11441d;
--color-forengers-white: #f2f2f3;
--color-forengers-gray: #686767;
--color-forengers-black: #232324;
```

Tailwind automatically converts these into usable utilities like:

- `bg-forengers-dark-green`
- `text-forengers-light-green`
- `border-forengers-gray`

This means **you never write hex codes directly inside components.**

---

## Available Forengers Brand Colors

Here are the main custom colors defined in our theme:

| Variable Name | Hex Value | Usage |
|---------------|-----------|--------|
| `--color-forengers-dark-green` | `#11441d` | Primary brand color — navbar, headings, brand sections |
| `--color-forengers-light-green` | `#347c05` | Accent color — buttons, highlights |
| `--color-forengers-white` | `#f2f2f3` | Off-white used across backgrounds |
| `--color-forengers-gray` | `#686767` | Neutral text, secondary UI elements |
| `--color-forengers-black` | `#232324` | Deep backgrounds and dark sections |

These colors are intentionally curated to maintain a consistent brand identity.

---

## How to Use These Colors in Components

### 🔹 Background Colors
```html
<div class="bg-forengers-dark-green">
```

### 🔹 Text Colors
```html
<p class="text-forengers-light-green">
```

### 🔹 Border Colors
```html
<div class="border border-forengers-gray">
```

### 🔹 Hover States
```html
<button class="bg-forengers-light-green hover:bg-forengers-dark-green">
```

### 🔹 Combined Utilities
```html
<div class="text-forengers-dark-green bg-forengers-white border border-forengers-light-green">
```

Because these are Tailwind theme variables, they work just like any built-in utility.

---

## Dark Mode Support

The file also includes custom dark-mode color overrides using:

```css
.dark {
  --background: ...;
  --foreground: ...;
}
```

Your components will automatically switch colors when using utilities like:

```html
<div class="bg-background text-foreground">
```

No manual theming is required.

---

## Best Practices for Contributors

### ✅ **DO use Tailwind utilities referencing our variables**
```html
text-forengers-dark-green
bg-forengers-light-green
```

### ❌ **DO NOT use raw hex codes inside components**
```html
/* Avoid */
color: #11441d;
```

### ❌ **Do not add random new brand colors**
If a new color is needed, ask the design lead or request a variable addition.

### ✅ Keep styling atomic  
Avoid writing custom CSS unless necessary—use Tailwind utilities.

### ✅ Maintain semantic usage  
Use dark green for primary brand elements, light green for actions/accents.


