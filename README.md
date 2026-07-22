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

Since v0.5.1, Tholos **updates itself in place**. On launch, the app checks for a newer release, downloads it in the background, and shows an in-app banner when it's ready — nothing installs until you click:

- **Windows** — click **Restart to update** to relaunch into the updater.
- **Linux** — click **Install update** and your desktop's package installer takes over (it asks for your password as usual).

Running v0.5.0 or older? Those builds have no updater — upgrade once manually from the [Releases](../../releases/latest) page, and every version after that updates in place. Your notebook is stored separately and is never touched by an update.

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
- 🧠 **Agent memory** *(new in 0.6.0)* — opt-in: let your agent remember facts and preferences across sessions, with full inspect/forget/clear control in Settings.
- 📚 **Reference corpora** — index an external repo or docs folder locally; connected agents search it semantically and cite `file:line` instead of re-reading files.
- 🎨 **Themes** — light/dark, accent color, and density options.

### Agent memory & the Persona (new in 0.6.0)

Normally a connected agent starts every session from scratch — you re-explain your preferences each time. With **Agent memory** enabled, an MCP client like Claude Code can save what's worth keeping and recall it in later sessions:

- **Memories** — short, atomic facts the agent distills as you work ("files meeting notes under Work", "prefers terse summaries"), recalled by semantic search at the start of a task.
- **The Persona** — a single short document describing your stable working style, which the agent refines over time as it gets to know you.

The feature is designed to stay in your hands:

- **Off by default.** Enable it under **Settings → Agent memory**. While it's off, every memory tool call is refused — nothing accumulates without your consent.
- **Reviewable in Settings.** List every saved memory, read the Persona, **Forget** individual memories, or **Clear all**.
- **Local, plain, and per-notebook.** Memories are human-readable files inside your notebook's data folder — nothing is uploaded by Tholos, and each notebook keeps its own independent memory store.

How it works, briefly:

- **The agent is the author.** Your AI client decides what's worth keeping and saves one distilled sentence at a time; Tholos only stores and retrieves — it never sees your conversation.
- **Recall is hybrid local search** — the same on-device semantic + keyword engine that powers reference corpora (below), so a relevant memory surfaces even when the wording differs.
- **Plain files on disk.** Memories and the Persona are human-readable files in your notebook's data folder — you can audit them with any text editor.
- The layered design — atomic memories beneath a single distilled persona, everything human-readable on disk — is inspired by Tencent's open-source [TencentDB-Agent-Memory](https://github.com/Tencent/TencentDB-Agent-Memory); Tholos implements the pattern natively on its own local search stack rather than embedding that project.

Tholos automatically teaches connected agents to use memory well (recall at task start, save distilled facts). To reinforce or customize those habits per-repo, see [docs/CLAUDE.md.example](docs/CLAUDE.md.example).

One trade-off to know: memories are saved by the agent and must stay readable to it, so — unlike locked sections — they are stored **unencrypted** on disk, and anything the agent recalls enters your AI client's context just like a note you've shared. If that trade-off isn't right for you, simply leave Agent memory off.

### Reference corpora — let your agent search a codebase instead of re-reading it

Point Tholos at a repository or docs folder (**Import ▾ → Reference corpora…**) and it builds a local semantic index. A connected agent can then *search* the corpus: one query returns the most relevant passages with `file:line` citations, so its answers stay grounded in the actual source at a fraction of the token cost of reading whole files.

- **Index once, query many times.** Reindex after the source changes — or remove a corpus — from the same dialog.
- **Fully local and offline.** Embeddings are computed on your machine by a bundled model; nothing is uploaded to build or search an index.
- **Per-notebook and removable.** Each corpus lives in one folder inside your notebook's data directory — one thing to delete, and deleting it never touches the source.
- **Never your notes.** Corpora index external folders you choose; Tholos does not build a semantic index over your notebook.

Corpus search is powered by [zvec](https://github.com/alibaba/zvec), an embedded vector database that ships with Tholos as an optional native component — on platforms where it isn't supported, the feature simply reports itself unavailable and the rest of Tholos is unaffected.

Connected agents are told to prefer corpus search automatically; [docs/CLAUDE.md.example](docs/CLAUDE.md.example) shows how to reinforce or customize this in a repo's own instructions.

### Handy shortcuts

| Action | Shortcut |
| --- | --- |
| Search all sections | `Ctrl+K` |
| Find in page | `Ctrl+F` |
| Toggle heading outline | `Ctrl+Shift+O` |
| Back / Forward | Mouse back/forward buttons |

## Privacy & your data

Tholos is **local-first**. Your notebook is stored in a local database on your computer — nothing is uploaded to a server. Locked sections are encrypted at rest and stay encrypted until you unlock them for the session. Agent memory (if you enable it) is also stored locally, in plain human-readable files you can review and delete from Settings at any time.

## System requirements

- **Windows** — Windows 10 or 11 (64-bit)
- **Linux** — a Debian-based x86-64 distribution (Ubuntu 22.04+ or equivalent)

## Reporting issues

Found a bug or have a request? Please [open an issue](../../issues).

## License & disclaimer

Tholos is distributed under the [MIT License](LICENSE).

**No warranty.** Tholos is provided **"as is"**, without warranty of any kind, express or implied, including but not limited to the warranties of merchantability, fitness for a particular purpose, and noninfringement. In no event shall the authors or copyright holders be liable for any claim, damages, or other liability arising from, out of, or in connection with the software or its use.

**You assume all risk.** You are solely responsible for how you use Tholos and for the safekeeping of your data. That includes keeping **backups of your notebook** and remembering the **passphrases for locked sections** — encrypted content cannot be recovered without its passphrase. Content produced or modified by connected AI agents is your responsibility to review.

## Built with

- [zvec](https://github.com/alibaba/zvec) — embedded vector search engine behind reference corpora and memory recall
- [bge-small-en-v1.5](https://huggingface.co/Xenova/bge-small-en-v1.5) on [transformers.js](https://github.com/huggingface/transformers.js) — fully local, offline embeddings
- [TencentDB-Agent-Memory](https://github.com/Tencent/TencentDB-Agent-Memory) — design inspiration for the layered agent-memory model

---

<sub>© 2026 Cody Pinto. Tholos is distributed under the MIT License, as-is and without warranty of any kind.</sub>
