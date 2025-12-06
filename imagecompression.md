---
title: Image Compression Utility
description: How to use the CompressImages.ipynb script to compress images to WebP / AVIF and produce a zip of outputs.
layout: libdoc_page.liquid
permalink: imagecompression.html
tags:
    - image
    - compression
    - webp
    - avif
tocEnabled: false
date: false
eleventyNavigation:
    key: image compression
---

## Table of Contents
1. [Overview](#overview)
2. [Quick Process](#quick-process)
3. [Prerequisites](#prerequisites)
4. [How it works](#how-it-works)
5. [Usage — step-by-step](#usage--step-by-step)
6. [Function parameters & options](#function-parameters--options)
7. [Example: run in a notebook / script](#example-run-in-a-notebook--script)
8. [Output structure & download](#output-structure--download)
9. [Troubleshooting & tips](#troubleshooting--tips)
10. [License & credits](#license--credits)

---

## Overview

This page documents **CompressImages.ipynb** — a small utility that resizes and converts images from an `input/` folder into compressed WebP (and optionally AVIF) files in an `output/` folder, and finally zips the outputs.

**The goal:** quick, reproducible, and configurable compression for large image batches.

---

## Quick Process

1. Create two folders at repo root: `input/` and `output/`.
2. Put source images into `input/`. Accepts: `.jpg`, `.jpeg`, `.png`, `.bmp`, `.tiff`, `.gif`, `.webp`.
3. Run the script (or run all notebook cells).
4. After completion, an `images.zip` file containing the compressed images is generated.

---

## Prerequisites

The script relies on:

- Python with Pillow (PIL)
- `cwebp` CLI (for WebP conversion)
- `avifenc` CLI (optional, for AVIF conversion)

### Install on Debian/Ubuntu
```bash
sudo apt-get update
sudo apt-get install webp        # installs cwebp
sudo apt-get install libavif-bin # installs avifenc
```

### Install Python dependencies
```bash
pip install pillow
```

## How it works

The script iterates over files in `input_dir`.

For supported images it:

1. Opens with Pillow (PIL).
2. Resizes the image if either dimension > `max_dim` preserving aspect ratio (uses `Image.LANCZOS`).
3. Saves a temporary PNG file.
4. Calls `cwebp` with configured `webp_options` to write `<basename>.webp` into `output_dir`.
5. Optionally calls `avifenc` with `avif_options` to write `<basename>.avif`.
6. Removes the temporary PNG.

After all conversions a zip of the output folder is created (e.g. `images.zip`).

## Usage — step-by-step

### 1. Create folders

At the project root (or notebook working directory):
```bash
mkdir -p input output
# add images to input/
```

### 2. Configure and run

If you are using the provided notebook or running as a script, set parameters and call `compress_images(...)`. Example parameters are included below.

### 3. After completion

A zip is created:
```bash
zip -r images.zip output
```

Download or move `images.zip` as needed.

## Function parameters & options

Function signature:
```python
compress_images(
    input_dir,
    output_dir,
    max_dim=1000,
    cwebp_path="cwebp",
    avifenc_path="avifenc",
    avif=False,
    webp_options=None,
    avif_options=None,
)
```

- **`input_dir` / `output_dir`** — folders for source and converted files.
- **`max_dim`** — maximum width/height (pixels). Images larger than this are rescaled.
- **`cwebp_path` / `avifenc_path`** — path to the external CLI binaries.
- **`avif`** — boolean: when `True`, also produce AVIF files (requires `avifenc`).
- **`webp_options` / `avif_options`** — lists of additional CLI options passed to `cwebp` and `avifenc` respectively. Examples below.

### Recommended webp_options examples

- **High-quality WebP (variable):** `["-q", "90", "-m", "6"]`
- **More aggressive compression:** `["-q", "75", "-m", "6"]`

### Recommended avif_options example

Use constrained quality + speed:
```python
["--speed", "6", "--advanced", "end-usage=cq", "--advanced", "cq-level=20", "--advanced", "tune=ssim"]
```

Adjust levels to taste — test a few images to find acceptable quality/size trade-off.

## Example: run in a notebook / script

This is the core invocation used in the included notebook/script:
```python
input_dir = "input"
output_dir = "output"
start = time.time()
compress_images(
    input_dir,
    output_dir,
    max_dim=1300,
    avif=False,
    avif_options=[
        "--speed", "6",
        "--advanced","end-usage=cq",
        "--advanced", "cq-level=20",
        "--advanced", "tune=ssim"
    ],
    webp_options=["-q", "90", "-m", "6"]
)
print(f"\n\nCompletion Time: {(time.time() - start)/60} mins")
```

Notebook cells that zip output:
```bash
! rm -f images.zip
! zip -r images.zip output
```

## Output structure & download

Converted files are written as `<basename>.webp` (and optionally `<basename>.avif`) in `output/`.

Example:
```
input/
└── photo1.jpg

output/
└── photo1.webp
└── photo1.avif   # if avif enabled

images.zip
```

## Troubleshooting & tips

### cwebp / avifenc not found

Ensure the binaries are on PATH or pass absolute paths in `cwebp_path` / `avifenc_path`.

### Permission or install errors (notebook)

Use `sudo apt-get install webp libavif-bin` on Debian/Ubuntu in a Linux environment; in other environments install the corresponding packages or use container/VM.

### Large memory or slow conversions

- Use lower `max_dim`.
- Use faster encoding options (`--speed` for `avifenc`, lower `-q` for `cwebp`).
- Consider batching or running on a machine with more CPU.

### Bad image open errors

The script skips images Pillow cannot open and prints the exception — check file format and integrity.

### Quality check

Test on a handful of images with different `webp_options` / `avif_options` until you're happy with the size vs visual quality.

### Performance considerations

- AVIF often gives better compression than WebP but encoding can be significantly slower.
- For bulk processing, choose a balance of `--speed` (avif) and `-q` (webp) for throughput.
- Removing temporary files is handled by the script — ensure it has write permissions to the working folder.

## License & credits

The script uses Pillow (PIL) and platform CLI tools `cwebp` and `avifenc`.
