# AyuGram Static Linux Builder

This repository provides **automated static builds** of [AyuGram](https://github.com/AyuGram/AyuGramDesktop) for Linux (x86_64).  
It uses GitHub Actions to build the latest development version and also creates stable releases when new tags appear in the official repository.

> **Note:** The binaries are statically linked and should run on most modern Linux distributions without requiring extra dependencies.

## What's Inside

- **Stable releases** – built from official version tags (e.g., `v7.0.9`) and published as a GitHub Release.
- **Nightly builds** – built from the latest `dev` branch every 6 hours, published as a pre‑release called `nightly`.

Both are packaged as `.tar.xz` archives containing a single `Ayugram/` folder with the executable inside.

## How It Works

The GitHub Actions workflow (`.github/workflows/build-linux.yml`) does the following:

1. **Clones** the official `AyuGram/AyuGramDesktop` repository (with submodules).
2. **Detects** the latest tag (for stable) and the current commit hash (for nightly).
3. **Builds** using the official Docker image (`ghcr.io/telegramdesktop/tdesktop/centos_env`) with LTO enabled.
4. **Strips** debug symbols and packages the binary as a `.tar.xz` archive.
5. **Publishes**:
   - The **stable** release if the tag hasn't been released before.
   - The **nightly** pre‑release (re‑created on every run) with the commit hash in the filename.

The workflow runs automatically every 6 hours, ensuring fresh nightly builds and detecting new upstream tags.

## Releases & Downloads

- [**Stable releases**](https://github.com/fadlyandryanto/Ayugram-Builds/releases) – versioned, stable.
- [**Nightly builds**](https://github.com/fadlyandryanto/Ayugram-Builds/releases/tag/nightly) – always the latest `dev` (pre‑release).

### Manual Trigger

You can also trigger a build manually from the **Actions** tab by selecting the workflow and clicking **Run workflow**.

## System Requirements

- **OS**: Linux (x86_64)
- **glibc**: 2.17 or newer (typical for CentOS 7 / RHEL 7 and later)
- **No additional libraries** – the binary is statically linked.

## Usage

Download the archive, extract, and run:

```bash
# Example for a stable release
tar -xJf ayugram-7.0.9-x86_64.tar.xz
cd Ayugram
./AyuGram

# Example for nightly
tar -xJf ayugram-desktop-git-a1b2c3d-x86_64.tar.xz
cd Ayugram
./AyuGram
```

## Credits

- [AyuGram](https://github.com/AyuGram/AyuGramDesktop) – the original project.
- This builder is not affiliated with the AyuGram team; it's a community‑driven automation.

## License

The binaries are built from open‑source code and inherit the license of the original project (GPLv3).  
This repository contains only workflow definitions and documentation.

## Issues & Feedback

If you encounter problems with the build process, please [open an issue](https://github.com/fadlyandryanto/Ayugram-Builds/issues). For bugs in AyuGram itself, report them to the [upstream repository](https://github.com/AyuGram/AyuGramDesktop/issues).
