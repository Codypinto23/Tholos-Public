# Tholos

**A local-first Markdown notebook for Windows.** Organize notes into sections and pages, search everything instantly, lock sensitive sections behind a passphrase, and let an AI agent help — all stored locally on your machine.

> 📦 **This repository hosts the release builds for Tholos.** The application source is maintained privately; this page is for downloading the app and receiving updates.

---

## Download & Install

1. Go to the [**Releases**](../../releases/latest) page and download the latest `Tholos-<version>-setup.exe`.
2. Run the installer. Tholos installs per-user — **no administrator rights required**.
3. Launch Tholos from the Start Menu or desktop shortcut.

### "Windows protected your PC" warning

Current builds are **not yet code-signed**, so Windows SmartScreen may warn you on first launch. To proceed:

1. Click **More info**.
2. Click **Run anyway**.

This only happens until the app is signed.

## Updates

Once installed, Tholos checks for new versions and updates itself — you don't need to download installers manually after the first time. Just keep using the app; new releases are applied automatically.

## Features

- 📝 **Sections & pages** — a two-level notebook (pages with subpages), drag to reorder and move.
- ✍️ **Markdown editor** — Write / Split / Preview modes with live rendering and syntax-highlighted code blocks.
- 🔎 **Full-text search** across all sections (`Ctrl+K`), with every match on a page surfaced and jumpable.
- 🔦 **In-page find** (`Ctrl+F`) and a **heading outline** navigator (`Ctrl+Shift+O`).
- 🔐 **Encrypted sections** — lock a section with a passphrase; contents are encrypted at rest, with idle auto-lock.
- 🗑️ **Trash** — soft-delete pages and sections, then restore or empty.
- 📥 **Import / export** — import Markdown files, import a whole folder as a new section, and export back to Markdown.
- 🤖 **AI agent access** — connect an MCP-compatible client (e.g. Claude Code) to read and edit notes you've opted in.
- 🎨 **Themes** — light/dark, accent color, and density options.

### Handy shortcuts

| Action | Shortcut |
| --- | --- |
| Search all sections | `Ctrl+K` |
| Find in page | `Ctrl+F` |
| Toggle heading outline | `Ctrl+Shift+O` |
| Back / Forward | Mouse back/forward buttons |

## Privacy & your data

Tholos is **local-first**. Your notebook is stored in a local database on your computer — nothing is uploaded to a server. Locked sections are encrypted at rest and stay encrypted until you unlock them for the session.

## System requirements

- Windows 10 or 11 (64-bit)

## Reporting issues

Found a bug or have a request? Please [open an issue](../../issues).

---

<sub>© <year> <your name / org>. Tholos is distributed as-is.</sub>
