# Tholos

**A local-first Markdown notebook for Windows and Linux.** Organize notes into sections and pages, search everything instantly, lock sensitive sections behind a passphrase, and let an AI agent help — all stored locally on your machine.

> 📦 **This repository hosts the release builds for Tholos.** The application source is maintained privately; this page is for downloading the app.

---

## Download & Install

Grab the build for your platform from the [**Releases**](../../releases/latest) page.

### Windows

1. Download `Tholos-<version>-setup.exe`.
2. Run the installer. Tholos installs per-user — **no administrator rights required**.
3. Launch Tholos from the Start Menu or desktop shortcut.

#### "Windows protected your PC" warning

Current builds are **not yet code-signed**, so Windows SmartScreen may warn you on first launch. To proceed:

1. Click **More info**.
2. Click **Run anyway**.

This only happens until the app is signed.

### Linux (Debian / Ubuntu)

1. Download `Tholos-<version>-amd64.deb`.
2. Install it with apt, which pulls in the required GTK/NSS libraries:

   ```sh
   sudo apt install ./Tholos-<version>-amd64.deb
   ```

3. Launch Tholos from your application menu, or run `tholos-notes` from a terminal.

## Updates

Tholos does **not** update itself. When a new version ships, download the latest installer from the [Releases](../../releases/latest) page and run it over your existing install — your notebook is stored separately and is left untouched.

Watch this repository (**Watch → Custom → Releases**) to get notified when a new version is published.

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

- **Windows** — Windows 10 or 11 (64-bit)
- **Linux** — a Debian-based x86-64 distribution (Ubuntu 22.04+ or equivalent)

## Reporting issues

Found a bug or have a request? Please [open an issue](../../issues).

---

<sub>© 2026 Cody Pinto. Tholos is distributed as-is.</sub>
