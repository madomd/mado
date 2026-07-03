# Mado

**AI writes Markdown. Mado makes it readable.**

https://madomd.com

Mado is a native macOS app for reading AI-generated Markdown — opening a plan, spec, report, or set of notes as a polished document, moving through folders of them, and sharing a clean page when the work is ready.

Writing got faster; reading got harder. AI tools produce implementation plans, product specs, design notes, meeting summaries, and reports in seconds — but people still have to read them carefully, make decisions, and pass them along. Markdown is excellent for generation and storage. Mado is built for the reading step that comes next.

Mado is **reading-first**. It renders Markdown as a document with clear typography, spacing, syntax highlighting, images, tables, task lists, and frontmatter. Lightweight **Source**, **Visual**, and **Split** editing is there when you need it, but the default experience stays focused on reading. Mado is not trying to replace VS Code, Obsidian, or a full writing environment.

It is designed around plain Markdown files in a folder-based **Workspace**. Open any folder and Mado presents it as a live file tree; opening an individual Markdown file never changes the current Workspace.

Open a Workspace with **File ▸ Open Folder…** (⇧⌘O), the titlebar **＋**, by dragging a folder onto the window, or from the CLI:

```sh
mado .
```

The current Workspace is remembered across launches. Reading and editing local files stays local-first: Markdown saves use atomic writes, with no telemetry or background sync. Optional Pro **sharing** publishes a page only when you explicitly send a document to a destination.

## Features

Mado is organized around four things you do with an AI-generated document: **read** it, **navigate** to it, **present** it, and **share** it. Editing is available reading-first, one keystroke away.

### Reading

- Document-first rendering with clear typography, spacing, and a reading-focused layout.
- Markdown frontmatter support, collapsible metadata rendering, GFM raw HTML preservation, and GFM `<details>` handling.
- Local image rendering for file paths and file URLs.
- Theme-aware code block highlighting for JavaScript, Python, Rust, Go, Ruby, Java, Markdown, Bash, Zig, C, C++, Makefile, HTML, CSS, JSON, TOML, YAML, and Swift.
- Theme switching from the Command Palette or **View ▸ Themes…**, with selected rows in the sidebar and palette styled from the active theme.

### Navigation

- Folder-based Workspace sidebar with expand/collapse, live filesystem updates, search, and automatic reveal of the current file.
- Sidebar file actions: New File (⌘N), New Folder, inline Rename, Duplicate, drag-to-move inside the Workspace, Reveal in Finder, and recoverable Move to Trash with Undo (⌘Z).
- Sidebar keyboard navigation while focused: ↑/↓ selection, ←/→ collapse or expand folders, Return rename, Space open, ⌘D duplicate, and ⌘⌫ move to Trash.
- Command Palette with Recents (⌘Y), Commands (⌘⇧P), and Themes modes, all backed by one shared action catalog.
- Recents and Favorites to return to important work.

### Presentation (Pro)

- Premium document presentations with designed typography, spacing, and layouts built for professional reading — e.g. **Brief**, **Ink**, and **Cadence**.
- Preview before export, then export with the selected presentation.
- Turns raw AI output into something you can send to a teammate, client, reviewer, or finance partner.

### Sharing

- Standalone **HTML** and **PDF** export that follows the on-screen theme, font size, content width, and table layout setting. PDF export uses the system print operation path, so long documents are paginated and wide content is scaled to page width.
- One-click share to a readable hosted link — built-in **Connectors** for Mado Pages, CodeSandbox, and PageDrop — so others see the same document without installing Mado.
- Add your own destination with a **Connector**: an *export destination* defined by a small `mado.json` manifest plus a `run.js` script (not a general plugin platform). See the connector developer guide on the website.
- Manage shared pages — copy the link, open it, or reclaim it.

### Editing

Reading-first, but full editing is one keystroke away:

- **Source**: edit the Markdown source directly, with tree-sitter backed syntax highlighting.
- **Visual**: edit a rendered rich-text document backed by the same Markdown buffer.
- **Split**: edit Source on the left and Visual on the right, with shared content and synchronized scroll progress.
- WYSIWYG Markdown triggers for headings, list items, and fenced code input.
- Open, Save, Save As, and drag-and-drop Markdown or folder opening.
