# Research Scaffold

A CLI-first, git-native framework for academic research. Fork this repo, run one command, and start finding, organizing, and citing sources — entirely from the terminal.

No GUIs. No subscriptions. Just plain text, git, and the command line.

## Quick Start

```bash
# 1. Fork/clone this repo
gh repo fork claycantrell/cognitive-augmentation-ai-era --clone

# 2. Install all tools
./setup.sh

# 3. Fill in your research topic
$EDITOR outline.md

# 4. Start finding papers
make search QUERY="your research topic"
```

## Repository Structure

```
├── manuscript/             # Your paper (Pandoc-ready Markdown)
│   └── main.md             # Manuscript template with YAML frontmatter
├── sources/                # Downloaded PDFs
├── library/                # Papis-managed references (YAML + PDFs)
├── notes/                  # Reading notes per source
├── bibliography/
│   ├── references.bib      # BibTeX file (auto-generated or manual)
│   └── citation-style.csl  # APA 7th edition (swap for any CSL style)
├── figures/                # Charts, diagrams, images
├── scratch/                # Brainstorming (git-ignored)
├── output/                 # Generated PDFs, DOCX, HTML (git-ignored)
├── templates/              # Note and section draft templates
├── scripts/                # Helper scripts for batch operations
├── docs/                   # Tool documentation by workflow stage
├── outline.md              # Research outline template
├── Makefile                # All commands in one place
└── setup.sh                # One-command installer
```

## Toolkit

Every tool is free and works from the command line.

| Stage | Tool | What It Does |
|-------|------|-------------|
| **Discovery** | [`semantic_bibtool`](https://github.com/rdyro/semantic_bibtool) | Search 200M+ papers, export BibTeX |
| | [`semanticscholar`](https://github.com/danielnsilva/semanticscholar) | Python API for deeper Semantic Scholar queries |
| **Retrieval** | [`arxiv-dl`](https://github.com/MarkHershey/arxiv-dl) | Download papers from arXiv by URL or ID |
| | [`doi2pdf`](https://pypi.org/project/doi2pdf/) | Download any paper by DOI |
| | [`pdf2doi`](https://github.com/MicheleCotrufo/pdf2doi) | Extract DOI from PDFs you already have |
| **Summarization** | [`slurp`](https://github.com/0v00/slurp) | Fetch, rank, and summarize arXiv papers |
| | [`arxiv-summarizer`](https://pypi.org/project/arxiv-summarizer/) | Summarize papers using local models |
| | [`scite-cli`](https://github.com/OpenDevEd/scite-cli) | Check if papers are supported or contradicted |
| **PDF Extraction** | `pdftotext` | Fast text extraction (via poppler) |
| | [`pdfminer.six`](https://pdfminersix.readthedocs.io/) | Layout-aware extraction for complex PDFs |
| **References** | [`papis`](https://github.com/papis/papis) | CLI reference manager — stores as plain YAML + PDFs |
| **Note-Taking** | [`nb`](https://xwmx.github.io/nb/) | Notes, bookmarks, wiki-links, git sync |
| | [`zk`](https://github.com/zk-org/zk) | Zettelkasten with markdown and sqlite search |
| **Publishing** | [`pandoc`](https://pandoc.org/) | Markdown → PDF / DOCX / HTML with auto-citations |

## Makefile Commands

Run `make` or `make help` to see all targets.

### Discovery
```bash
make search QUERY="cognitive enhancement"     # Search Semantic Scholar
make search-py QUERY="nootropics"             # Deeper Python-based search
```

### Retrieval
```bash
make fetch-arxiv ID="2301.00001"              # Download from arXiv
make fetch-doi DOI="10.1038/s41586-020-2649-2"  # Download by DOI
```

### PDF Processing
```bash
make extract-text PDF="sources/paper.pdf"     # Extract text from one PDF
make extract-all                              # Extract text from all PDFs
make identify-doi PDF="sources/paper.pdf"     # Find DOI in a PDF
```

### Summarization & Verification
```bash
make summarize PDF="sources/paper.pdf"        # AI-summarize a paper
make verify DOI="10.1038/s41586-020-2649-2"   # Check citation support/contradiction
```

### Reference Management
```bash
make add-paper DOI="10.1038/s41586-020-2649-2"  # Add to papis library
make add-pdf PDF="sources/paper.pdf"             # Add local PDF to library
make bib                                         # Export library → references.bib
make list-refs                                   # List all references
```

### Note-Taking
```bash
make new-note TITLE="Attention Is All You Need"  # Create reading note from template
make search-notes QUERY="transformer"             # Search across all notes
```

### Writing & Building
```bash
make pdf          # Build manuscript → PDF (with auto-citations)
make docx         # Build manuscript → Word
make html         # Build manuscript → HTML
make all          # Build all formats
make wordcount    # Count words in manuscript
```

## Workflow

```
1. Define       → Edit outline.md with your research question
2. Discover     → make search QUERY="..."
3. Retrieve     → make fetch-doi DOI="..." / make fetch-arxiv ID="..."
4. Store        → make add-paper DOI="..."
5. Extract      → make extract-text PDF="..."
6. Summarize    → make summarize PDF="..."
7. Verify       → make verify DOI="..."
8. Note         → make new-note TITLE="..."
9. Write        → Edit manuscript/main.md (cite with [@key] syntax)
10. Build       → make bib && make pdf
11. Iterate     → Repeat steps 2-10
```

See [docs/workflows.md](docs/workflows.md) for a detailed walkthrough.

## Writing with Citations

Write your manuscript in `manuscript/main.md` using standard Markdown. Cite sources with Pandoc's citation syntax:

```markdown
Recent work suggests cognitive enhancement is inevitable [@smith2024].
This aligns with earlier findings [@jones2023, p. 42].
Multiple studies confirm this trend [see @smith2024; @jones2023; @doe2022].
```

When you run `make pdf`, Pandoc automatically:
- Resolves `[@key]` citations against `bibliography/references.bib`
- Formats them in APA 7th edition (or whatever CSL style you choose)
- Appends a formatted References section

Swap citation styles by replacing `bibliography/citation-style.csl` with any file from the [Zotero Style Repository](https://www.zotero.org/styles).

## API Keys

Some tools require free API keys. After running `setup.sh`, edit `.env`:

| Key | Required? | Get it at |
|-----|-----------|-----------|
| `SEMANTIC_SCHOLAR_API_KEY` | Recommended | [semanticscholar.org/product/api](https://www.semanticscholar.org/product/api#Partner-Form) |
| `OPENAI_API_KEY` | Optional (for slurp AI summaries) | [platform.openai.com](https://platform.openai.com) |
| `ANTHROPIC_API_KEY` | Optional (alternative for slurp) | [console.anthropic.com](https://console.anthropic.com) |

## Documentation

Detailed tool guides organized by workflow stage:

- [01 — Discovery](docs/01-discovery.md) — Finding papers
- [02 — Retrieval](docs/02-retrieval.md) — Downloading papers
- [03 — Summarization](docs/03-summarization.md) — Understanding papers
- [04 — PDF Extraction](docs/04-pdf-extraction.md) — Extracting text
- [05 — Reference Management](docs/05-reference-management.md) — Managing your library
- [06 — Note-Taking](docs/06-note-taking.md) — Structured notes
- [07 — Writing & Publishing](docs/07-writing-and-publishing.md) — Building your manuscript
- [End-to-End Workflow](docs/workflows.md) — Complete walkthrough

## Contributing

See [CONTRIBUTING.md](CONTRIBUTING.md). PRs welcome — especially new CLI tools, better scripts, and cross-platform fixes.

## License

MIT — see [LICENSE](LICENSE).
