---
hide:
  - navigation
  - toc
---

# Contributing to the Docs

Thanks for helping keep the Team Rudra docs up to date. This page captures the minimum workflow for local previews and the conventions we follow when writing content for MkDocs Material.

## Local preview on `localhost:8000`

- Install Python 3.10+.
- From the workspace root run the **VS Code Task `mkdocs serve (venv auto-setup)`** (`⇧⌘B`/`Ctrl+Shift+B` → pick the task). (can be run from cmd_line, zed, neovim as well) The task will:
    1. Create `.venv` if it does not exist.
    2. Install `requirements.txt`.
    3. Launch `mkdocs serve --livereload` that watches the repo and serves the site at <http://localhost:8000>.
- Prefer this task—it keeps every contributor on the same dependency set and avoids editing your global Python packages.

Stop the server with `Ctrl+C` in the terminal where the task ran.

## Writing documentation

- **Docs live in `md-pages/`.** Keep filenames descriptive (lowercase with dashes or underscores) so generated URLs stay readable.
- **Navigation is controlled by `.pages`.** Each folder that needs ordering or custom titles has a `.pages` file.
  - Example (`md-pages/.pages`):

```yaml
nav:
  - index.md
  - ROS: ros
  - perception
  - contributing.md
```

  `ROS: ros` renders the nav label `ROS` while sourcing files from the `ros/` directory. When you add or rename a page, update the `.pages` in that folder to keep navigation deterministic.

- **Create indexes.** Every new section folder should include an `index.md` so MkDocs Material can render section landing pages and breadcrumb trails correctly. Not mandatory but recommended.
- **Use MkDocs Material features.** All Markdown is processed through Material’s extensions (admonitions, tables, callouts, etc.). Keep content lightweight but structured with headings, numbered steps, and callouts (`!!! note`, `!!! warning`) where they help the reader.
- **Code and math.** Prefer fenced code blocks with explicit languages (```` ```bash ````). MathJax is preloaded, so inline `$math$` and block `$$ math $$` render correctly.
- **Image Size**: Resize images to keep them small. This reduces the size bloat added to the documentation causing the pull size to drastically increase everytime contributions are made.

## Before you open a PR

- Preview locally and ensure there are no MkDocs build warnings.
- Check navigation (tabs, sidebar) for your new content and confirm the order matches `.pages`.
- Spell-check and lint manually—there is no CI spell checker yet.
- Keep commits scoped to documentation changes so reviewers can land them quickly.
- Commit title's must be small-case only excepting proper nouns and present tense with the format: 
  (scope): description.
  
    **Example:**
    >rtos: add new section for FreeRTOS

Feel free to add process improvements here whenever you refine the workflow.***
