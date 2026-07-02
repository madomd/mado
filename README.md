# Mado

https://madomd.com

Mado is a local-first macOS SwiftUI Markdown editor with three editing layouts:

- **Source**: edit the Markdown source directly.
- **Visual**: edit a rendered rich-text document backed by the same Markdown buffer.
- **Split**: edit Source on the left and Visual on the right, with shared content and synchronized scroll progress.

It is designed around plain Markdown files in a folder-based **Workspace**. Open any folder and Mado presents it as a live file tree; opening an individual Markdown file never changes the current Workspace.

Open a Workspace with **File ▸ Open Folder…** (⇧⌘O), the titlebar **＋**, by dragging a folder onto the window, or from the CLI:

```sh
mado .
mado ~/Documents/Notes
```

The current Workspace is remembered across launches. Mado does not add sync, telemetry, remote storage, or network behavior; Markdown saves use atomic writes.

## Features

- Folder-based Workspace sidebar with expand/collapse, live filesystem updates, search, and automatic reveal of the current file.
- Sidebar file actions: New File (⌘N), New Folder, inline Rename, Duplicate, drag-to-move inside the Workspace, Reveal in Finder, and recoverable Move to Trash with Undo (⌘Z).
- Sidebar keyboard navigation while focused: ↑/↓ selection, ←/→ collapse or expand folders, Return rename, Space open, ⌘D duplicate, and ⌘⌫ move to Trash.
- Command Palette with Recents (⌘Y), Commands (⌘⇧P), and Themes modes, all backed by one shared action catalog.
- Markdown source editing with tree-sitter backed syntax highlighting.
- Visual editing backed by Markdown serialization.
- Split editing with shared Markdown content and synchronized scroll progress.
- WYSIWYG Markdown triggers for headings, list items, and fenced code input.
- Markdown frontmatter support, collapsible metadata rendering, GFM raw HTML preservation, and GFM `<details>` export handling.
- Local image rendering for file paths and file URLs.
- Code block highlighting and source-mode fenced-code highlighting for JavaScript, Python, Rust, Go, Ruby, Java, Markdown, Bash, Zig, C, C++, Makefile, HTML, CSS, JSON, TOML, YAML, and Swift.
- Theme switching from the Command Palette or **View ▸ Themes…**, with selected rows in the sidebar and palette styled from the active theme.
- Open, Save, Save As, Export HTML, Export PDF, and drag-and-drop Markdown or folder opening.
- HTML/PDF export that follows the on-screen theme, font size, content width, and table layout setting.
- PDF export uses the system print operation path so long documents are paginated and wide content is scaled to page width.

## Architecture

Mado keeps Markdown parsing and rendering separate from the SwiftUI interface:

- `MadoCore/Parser` owns Markdown parsing and turns a `swift-markdown` AST into a small render model (`RenderedMarkdown`, `MarkdownSpan`, `MarkdownBlock`).
- `MadoCore/Render` owns Markdown serialization, preview HTML, document fonts, content-width/table-layout settings, and export templates.
- `MadoCore/Storage` owns Workspace directory operations, recent-file metadata, and Markdown file IO.
- `MadoCore/Editing` owns shared editor state, document titles, frontmatter parsing, paste classification, sidebar visibility state, and WYSIWYG Markdown triggers.
- `MadoCore/Highlighter` owns the tree-sitter language registry and shared highlighting API.
- `MadoCore/Theme` owns GPUI theme loading and the color roles shared by the app chrome, editors, sidebar, Command Palette, preview, and export.
- `Mado` owns the macOS SwiftUI shell, Workspace sidebar, Command Palette, menu/action wiring, drag-and-drop open, source editor, and TextKit-based visual editor.
- `MadoActionCatalog` is the single source for menu commands, Command Palette entries, and keyboard shortcuts.
- `swift-markdown` is the parser dependency. Mado renders the AST itself so the editor can grow toward editable tables, task lists, custom blocks, and other long-term Markdown features without being tied to a read-only Markdown view.
- Export is template-driven through `MarkdownExportTemplate`; `BasicHTMLTemplate` powers visual HTML export and `FileHTMLExportTemplate` wraps complete export documents.
- Syntax highlighting uses `swift-tree-sitter` and local grammar query bundles. Markdown source highlighting uses the Markdown grammar directly, while fenced code blocks use Markdown injection queries to route content into the matching language grammar.

`Textual` is a good candidate for a later high-quality read-only preview surface, but this first editor path keeps the WYSIWYG editor on `NSTextView` because it needs editable rich text and Markdown write-back.

## Development

Resolve dependencies and run tests:

```sh
swift test
```

Run the development app:

```sh
swift run
```
