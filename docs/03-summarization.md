# Understanding Papers

Tools for summarizing, ranking, and verifying academic papers.

---

## slurp

Fetch, rank, and summarize arXiv papers using AI (OpenAI or Anthropic).

### Install

Install from GitHub -- the PyPI package named `slurp` is an unrelated project:

```bash
pip install git+https://github.com/0v00/slurp.git
```

### API Key

Requires an LLM API key for AI-powered summaries. Set one of these in `.env`:

```bash
OPENAI_API_KEY=sk-...
# or
ANTHROPIC_API_KEY=sk-ant-...
```

Without an API key, slurp can still fetch and rank papers but will skip AI summaries.

### Examples

```bash
# Summarize recent papers on a topic
slurp "cognitive augmentation artificial intelligence"

# Limit to papers from the last 7 days
slurp "transformer architecture" --days 7

# Output as JSON for scripting
slurp "brain-computer interfaces" --format json

# Rank by relevance and summarize top 5
slurp "nootropics cognition" --top 5
```

### How it connects

- Summaries help you decide which papers to download (`make fetch-arxiv`) and import into your library (`make add-paper`).
- Use alongside your reading notes (`make new-note`) to capture key findings before diving into full papers.

---

## arxiv-summarizer

Summarize papers using local HuggingFace models. Runs entirely offline -- no API key needed.

### Install

```bash
pip install arxiv-summarizer
```

Downloads model weights on first run (may take a few minutes).

### Examples

```bash
# Summarize a local PDF
arxiv-summarizer sources/paper.pdf

# Summarize by arXiv ID
arxiv-summarizer 2301.00001

# Adjust summary length
arxiv-summarizer sources/paper.pdf --max-length 500
```

### Makefile shortcut

```bash
make summarize PDF="sources/paper.pdf"
```

Runs `arxiv-summarizer` on the given PDF and prints the summary to stdout.

### How it connects

- Good for quick triage: run on each PDF in `sources/` to decide which papers warrant a full reading note.
- Output can be pasted directly into the Summary section of a note created with `make new-note`.

---

## scite-cli

Check whether a paper's findings have been supported or contradicted by subsequent research (1.6B+ citation statements).

### Install

Clone and set up from GitHub (Node.js required):

```bash
git clone https://github.com/OpenDevEd/scite-cli.git /tmp/scite-cli
cd /tmp/scite-cli && npm run setup
```

The `setup.sh` script in this repo handles this automatically (installs to `~/.local/share/scite-cli`).

### API Key

Configure your scite access token:

```bash
scite-cli config set access-token
```

### Examples

```bash
# Look up citation context for a paper
scite-cli papers 10.1038/s41586-020-2649-2

# Check multiple papers at once
scite-cli papers 10.1002/bin.1697 10.1002/best.202271004

# Get tallies (supporting, contradicting, mentioning)
scite-cli tallies 10.1038/s41586-020-2649-2
```

### Makefile shortcut

```bash
make verify DOI="10.1038/s41586-020-2649-2"
```

Runs `scite-cli` with the given DOI and displays the citation context.

### How it connects

- Run before citing a paper to confirm its findings are well-supported.
- Pair with `make identify-doi` to extract the DOI from a PDF, then pipe it into `make verify`.
- Results inform your Discussion section and help strengthen your manuscript's argumentation.
