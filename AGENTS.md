# AGENTS.md

Use this guide for agentic changes in this repo.
Primary goal: keep resumes compiling with XeLaTeX and preserve template conventions.

## Repo Snapshot
- Resume sources are LaTeX files in the repo root (e.g., `Chandrakanth Reddy.tex`, `Chandrakanth-Qualcomm.tex`, `cuvette.tex`).
- Template logic lives in `resume-openfont.cls` and styling in `font-color.sty`, `lato-font.sty`, `raleway-font.sty`.
- Fonts are stored under `fonts/` and require XeLaTeX (fontspec).
- Generated artifacts include `*.pdf`, `*.aux`, `*.log`, `*.out`, `*.fls`, `*.fdb_latexmk`, `*.xdv`.

## Build / Lint / Test
### Build (single resume)
- Recommended: `latexmk -xelatex -interaction=nonstopmode -halt-on-error "Chandrakanth Reddy.tex"`.
- Direct: `xelatex "Chandrakanth Reddy.tex"`.
- Build another variant by swapping the filename (e.g., `Chandrakanth-Qualcomm.tex`, `cuvette.tex`).
### Build (all resumes)
- No script is provided; run the build command per `*.tex` file you care about.
### Clean
- `latexmk -C "Chandrakanth Reddy.tex"` removes aux/log/xdv files for that target.
### Lint
- No linting is configured in this repo.
- Optional if installed: `chktex "Chandrakanth Reddy.tex"` (single file).
### Tests
- No automated tests; treat a successful XeLaTeX build as the test.
- "Single test" == compile the specific resume file you changed.

## Editing Workflow
- Identify the target resume file first; avoid editing multiple variants unless requested.
- Keep changes minimal and localized to content; avoid reformatting unrelated sections.
- If you add a macro, document its parameters and keep it near the top of the file.
- After edits, compile the changed `.tex` file to confirm layout and fonts.
- Check for overfull/underfull box warnings in the `.log` and address them.

## Code Style Guide (LaTeX)
### Source of truth
- Keep resume content in the `.tex` files; keep reusable formatting in `resume-openfont.cls` or a `.sty`.
- If a macro is shared across multiple resumes, move it into the class or a dedicated `.sty` instead of duplicating.
- Avoid editing generated files (`*.aux`, `*.log`, `*.pdf`, etc.).
### Imports and packages
- Do not add `\usepackage` calls inside the resume `.tex` files; add packages in `resume-openfont.cls`.
- Keep XeLaTeX compatibility (this template relies on `fontspec`).
- When introducing a new package, note why and prefer minimal options.
### Formatting and spacing
- Use `\section{...}` for section headers and `\sectionsep` between sections.
- Use the provided list environment `tightemize` for bullets; avoid nested lists.
- Prefer `\\*` for forced line breaks where used in existing files.
- Keep indentation consistent (4 spaces inside list blocks).
- Keep lines reasonably short (around 120 chars) to ease diff review.
### Lists and tables
- Use `resumeSkillList` for skills blocks and `singleItem`/`doubleItem` for rows.
- Add a line break with `\\` between rows in the skills table.
- Avoid raw `tabular` in the resume body unless matching existing layout.
- For bullets, keep to 2-4 bullets per role or project to preserve layout.
### Profile header
- Keep the header block centered unless the tabular profile is explicitly requested.
- Update `\yourName`, `\yourEmail`, `\yourPhone`, `\githubUserName`, `\linkedInUserName` near the top of each resume.
- Use `\underline{...}` for visible link text to match existing styling.
- Avoid adding extra social links without checking spacing.
- Prefer short handles to avoid line wrapping in the header.
### Macros, naming, and "types"
- Define new helper commands with `\newcommand` and explicit argument counts.
- Document the argument order in a short comment above the macro (as existing files do).
- Follow existing naming patterns: lowerCamelCase for helpers (`\resumeHeading`) and UpperCamelCase for entry macros (`\Project`).
- Reuse existing commands for consistency: `\educationHeading`, `\Project`, `\resumeHeading`, `\courseWork`, `\teacherAssistant`.
### Content conventions
- Keep section titles in Title Case and match the existing ordering where possible.
- Use active voice; past tense for completed roles, present tense for ongoing roles.
- Keep bullets concise, one idea per bullet, and avoid paragraph-length bullets.
- Use `\textbf{...}` sparingly to highlight key terms, not whole sentences.
- Prefer numerals for metrics (e.g., "95%") and keep units consistent.
### Links and special characters
- Use `\href{https://...}{...}` for URLs; keep links HTTPS.
- Escape LaTeX specials (`& % $ # _ { } ~ ^` and `\\`) when used as literal characters.
- For underscores in visible text, use `\_` or wrap in `\texttt{...}`.
- If a URL is long, keep it in the link target and shorten the visible text.
### Fonts and colors
- Keep font configuration in `lato-font.sty` and `raleway-font.sty`.
- Place new font files under `fonts/` and update the font path variables.
- Color palette lives in `font-color.sty`; use existing color names.
- Avoid custom colors in resume files; centralize them in `font-color.sty`.
### Layout guardrails
- This template is tuned for a single page; watch for accidental page breaks.
- If text overflows, trim content before adjusting spacing macros.
- Fix overfull boxes by tightening wording or inserting manual line breaks.
- Do not change geometry values unless specifically requested.
### Error handling and troubleshooting
- Build with `-halt-on-error` to catch issues early.
- XeLaTeX errors about fonts usually mean missing files under `fonts/` or a mismatched font name.
- If compilation behaves oddly, clean with `latexmk -C` and rebuild.
- Check the `.log` file for missing packages or undefined control sequences.

## File Naming
- Existing resumes use both spaces and hyphens; follow an existing pattern when adding a new variant.
- Prefer descriptive suffixes for variants (e.g., `Name-Company.tex`).
- Keep filenames ASCII and avoid punctuation other than spaces, hyphens, and underscores.

## Generated Files
- Treat these as build outputs and avoid manual edits: `*.aux`, `*.fdb_latexmk`, `*.fls`, `*.log`, `*.out`, `*.xdv`, `*.pdf`.
- When committing, include sources and styles; include PDFs only if explicitly requested.
- If you must share a PDF, regenerate it from the matching `.tex` file.

## Cursor / Copilot Rules
- No `.cursor/rules/`, `.cursorrules`, or `.github/copilot-instructions.md` files were found in this repo.

## Quick Reference
- Build single file: `latexmk -xelatex -interaction=nonstopmode -halt-on-error "<file>.tex"`.
- Direct build: `xelatex "<file>.tex"`.
- Clean single file: `latexmk -C "<file>.tex"`.
- Optional lint: `chktex "<file>.tex"`.
- Template class: `resume-openfont.cls`.
- Colors: `font-color.sty`.
- Fonts: `lato-font.sty`, `raleway-font.sty`.

## Minimal Example
```tex
\section{Projects}
\Project{Example Project}{https://example.com}
\descript{Tech Stack}
\begin{tightemize}
    \item One concise accomplishment with a metric.
    \item Another accomplishment in active voice.
\end{tightemize}
\sectionsep
```

## Notes for Agents
- Prefer modifying existing sections over adding new ones unless requested.
- Keep commented-out sections intact if they serve as templates.
- Avoid introducing new dependencies without checking their XeLaTeX compatibility.
- If a change affects multiple resumes, state which files were updated.
- Default to ASCII text unless a non-ASCII character is essential (e.g., a proper noun).

## Current Resume Decisions (Chandrakanth Reddy.tex)
- Default target resume: `Chandrakanth Reddy.tex`.
- Summary section removed to keep single-page layout unless explicitly requested.
- Projects order: `Nurl` first, then `LLM Finetuning For Spam Detection`.
- Work Experience bullets emphasize impact; keep failure-injection scale (10-15 injections, 500-1,000 nodes) and ~16 hours/drill savings; MCP server ~100 incidents/month.
- Skills structured with Backend & APIs, Cloud & Infrastructure (Azure), Observability & Security, AI/ML, Core CS; keep ATS keywords (Kubernetes, OpenAPI/Swagger, JWT, Azure Service Bus, ARM, CI/CD, etc.).
- Link styling in header must stay underlined for email/LinkedIn/GitHub.
- Typography tweaks:
  - Body font set to Lato Regular (for darker, more legible text).
  - Section headers use Lato Regular (not Light) and are darker.
  - `\sectionsep` increased to 8pt for breathing room.
- Color palette (font-color.sty) is darker than default; titles remain darker than body.

## Troubleshooting Checklist
- Build fails with fontspec error: confirm you are using XeLaTeX or LuaLaTeX.
- Missing glyphs: verify the font files exist under `fonts/`.
- Overfull boxes: shorten text or insert a manual line break.
- Unexpected spacing: confirm `\sectionsep` placement and avoid extra `\\`.
- Broken links: ensure URLs are valid and properly escaped.

## Scope
- This guide is for the LaTeX template in this repository only.
- If you add scripts or build tooling in the future, update this file.

## Contact
- If unsure about layout choices, align with the most recent resume variant.
- Use the resume variant that most closely matches the target role.

## End
- Keep AGENTS.md up to date with new tooling or rules.
