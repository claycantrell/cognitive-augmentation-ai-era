# Research Scaffold

**A ready-made project folder for academic research — with tools that find papers, organize your sources, manage citations, and produce a finished document.**

If you've ever spent hours hunting through databases, copying citations by hand, wrestling with formatting, or losing track of which paper said what — this project automates all of that. You type simple commands, and the tools do the tedious work.

Everything here is **free** and runs on your computer. Nothing is stored in the cloud. Your research stays yours.

---

## What Is This, Exactly?

Think of it as a **pre-organized filing cabinet for a research project**, except it lives on your computer as a folder (called a "repository") and comes with built-in tools that can:

- **Search millions of academic papers** by topic or keyword
- **Download papers** directly to your project folder
- **Summarize papers** so you can quickly decide what's worth reading
- **Check whether a paper's findings have been confirmed or disputed** by later research
- **Keep track of all your sources** with structured metadata
- **Manage your bibliography** automatically
- **Take structured reading notes** with templates
- **Produce a finished PDF, Word document, or webpage** from your writing — with properly formatted citations and a reference list

You interact with it by typing short commands into a "terminal" (the text-based interface on your computer). No clicking through menus, no subscription software, no learning curve beyond the commands listed below.

---

## What You'll Need Before Starting

1. **A Mac or Linux computer** (Windows users can use [WSL](https://learn.microsoft.com/en-us/windows/wsl/install))
2. **A terminal** — already on your computer:
   - Mac: open "Terminal" from Applications > Utilities
   - Linux: usually called "Terminal" in your applications menu
3. **A GitHub account** (free) — sign up at [github.com](https://github.com) if you don't have one
4. **A text editor** — anything works. If you don't have a preference, [VS Code](https://code.visualstudio.com/) is free and beginner-friendly. You can also use TextEdit (Mac) or any plain-text editor.

That's it. The setup script handles everything else.

---

## Getting Started (Step by Step)

### 1. Get a copy of this project

Open your terminal and paste this command:

```bash
gh repo fork claycantrell/research-scaffold --clone
cd research-scaffold
```

This creates your own copy of the project on your computer.

### 2. Install the tools

```bash
./setup.sh
```

This will automatically download and install everything you need. It takes a few minutes the first time. You'll see a checklist at the end showing what was installed.

### 3. Set up your research topic

Open the file called `outline.md` in your text editor. You'll see placeholder text like `{{YOUR WORKING TITLE}}` — replace these with your own research question, thesis, and section plan. This is your living table of contents.

### 4. Start finding papers

```bash
make search QUERY="your topic here"
```

That's it. You're researching.

---

## How the Folder Is Organized

When you look inside this project, here's what each folder is for:

| Folder | What goes in it | Analogy |
|--------|----------------|---------|
| `manuscript/` | Your paper — the actual writing | Your typewriter |
| `sources/` | Downloaded PDFs of papers you've found | Your file drawer of photocopied articles |
| `library/` | Organized metadata for each source | Your card catalog |
| `notes/` | Your reading notes on individual papers | Your note cards |
| `bibliography/` | Your formatted reference list | Your bibliography cards |
| `figures/` | Charts, images, diagrams | Your illustration folder |
| `scratch/` | Brainstorming, rough ideas, discarded material | Your wastebasket (that you can dig through later) |
| `output/` | The finished product — PDF, Word doc, etc. | Your printer tray |
| `templates/` | Pre-made forms for notes and drafts | Your blank index cards |
| `docs/` | Instructions for each tool | Your reference manual |

---

## The Commands (Your Cheat Sheet)

Every command starts with `make` followed by a word. Type `make` by itself to see the full list.

### Finding Papers

| What you want to do | What you type |
|---------------------|---------------|
| Search for papers on a topic | `make search QUERY="climate change migration"` |
| Do a deeper search with citation counts | `make search-py QUERY="climate change migration"` |

### Downloading Papers

| What you want to do | What you type |
|---------------------|---------------|
| Download a paper from arXiv | `make fetch-arxiv ID="2301.00001"` |
| Download a paper by its DOI number | `make fetch-doi DOI="10.1038/s41586-020-2649-2"` |

**What's a DOI?** It's a permanent ID number for a published paper — like an ISBN for books. You'll find it on the first page of most journal articles. It usually starts with `10.` followed by numbers.

### Working with PDFs

| What you want to do | What you type |
|---------------------|---------------|
| Pull the text out of a PDF | `make extract-text PDF="sources/paper.pdf"` |
| Pull text from all your PDFs at once | `make extract-all` |
| Find the DOI of a paper from its PDF | `make identify-doi PDF="sources/paper.pdf"` |

### Understanding & Verifying Papers

| What you want to do | What you type |
|---------------------|---------------|
| Get an AI summary of a paper | `make summarize PDF="sources/paper.pdf"` |
| Check if a paper's claims have been supported or contradicted | `make verify DOI="10.1038/s41586-020-2649-2"` |

### Organizing Your Sources

| What you want to do | What you type |
|---------------------|---------------|
| Add a paper to your library by DOI | `make add-paper DOI="10.1038/s41586-020-2649-2"` |
| Add a PDF you already downloaded | `make add-pdf PDF="sources/paper.pdf"` |
| Generate your bibliography file | `make bib` |
| See all sources in your library | `make list-refs` |

### Taking Notes

| What you want to do | What you type |
|---------------------|---------------|
| Create a new reading note (from a template) | `make new-note TITLE="Name of the Paper"` |
| Search through your notes | `make search-notes QUERY="keyword"` |

### Writing & Producing Your Paper

| What you want to do | What you type |
|---------------------|---------------|
| Turn your manuscript into a PDF | `make pdf` |
| Turn it into a Word document | `make docx` |
| Turn it into a webpage | `make html` |
| Build all three at once | `make all` |
| Check your word count | `make wordcount` |

---

## How Citations Work

You write your paper in the file `manuscript/main.md` using plain text. When you want to cite a source, you put its reference key in brackets:

```
Studies have shown a link between sleep and memory consolidation [@walker2017].

This was confirmed by later work [@smith2023, p. 42].

Multiple researchers agree [see @walker2017; @smith2023; @jones2021].
```

When you type `make pdf`, the system automatically:

1. Looks up each `[@key]` in your bibliography file
2. Formats the citation in proper academic style (APA 7th edition by default)
3. Generates a complete "References" section at the end of your paper

**You never have to format a citation by hand.** If you want a different style (Chicago, MLA, Harvard, etc.), you can swap in a different style file — there are thousands available at the [Zotero Style Repository](https://www.zotero.org/styles).

---

## The Typical Research Workflow

Here's how a research session might go, from start to finish:

```
 1. Plan         Open outline.md, define your question and argument
 2. Search       make search QUERY="your topic"
 3. Download     make fetch-doi DOI="..." or make fetch-arxiv ID="..."
 4. Catalog      make add-paper DOI="..."
 5. Read         make extract-text PDF="..." or open the PDF
 6. Summarize    make summarize PDF="..."
 7. Verify       make verify DOI="..." (are the findings still accepted?)
 8. Take notes   make new-note TITLE="Paper Name"
 9. Write        Edit manuscript/main.md, citing with [@key]
10. Build        make bib && make pdf
11. Repeat       Go back to step 2 as your research deepens
```

A detailed walkthrough with examples is in [docs/workflows.md](docs/workflows.md).

---

## API Keys (Optional but Recommended)

Some search tools work better with a free API key. After running the setup, you'll have a file called `.env` where you can paste these in:

| Key | What it's for | Cost | Where to get it |
|-----|--------------|------|-----------------|
| `SEMANTIC_SCHOLAR_API_KEY` | Faster, unlimited paper searches | Free | [semanticscholar.org](https://www.semanticscholar.org/product/api#Partner-Form) |
| `OPENAI_API_KEY` | AI-powered paper summaries | Pay-per-use | [platform.openai.com](https://platform.openai.com) |
| `ANTHROPIC_API_KEY` | Alternative AI summaries | Pay-per-use | [console.anthropic.com](https://console.anthropic.com) |

The Semantic Scholar key is the only one you really need, and it's completely free.

---

## The Tools Under the Hood

You don't need to know how these work individually — the `make` commands handle everything. But if you're curious:

| What it does | Tool name | More info |
|-------------|-----------|-----------|
| Searches 200M+ academic papers | Semantic Scholar | [docs/01-discovery.md](docs/01-discovery.md) |
| Downloads papers from arXiv | arxiv-dl | [docs/02-retrieval.md](docs/02-retrieval.md) |
| Downloads papers by DOI | doi2pdf | [docs/02-retrieval.md](docs/02-retrieval.md) |
| Extracts DOIs from PDFs | pdf2doi | [docs/02-retrieval.md](docs/02-retrieval.md) |
| Summarizes papers with AI | slurp, arxiv-summarizer | [docs/03-summarization.md](docs/03-summarization.md) |
| Checks if findings are supported/disputed | scite-cli | [docs/03-summarization.md](docs/03-summarization.md) |
| Extracts text from PDFs | pdftotext, pdfminer | [docs/04-pdf-extraction.md](docs/04-pdf-extraction.md) |
| Manages your reference library | papis | [docs/05-reference-management.md](docs/05-reference-management.md) |
| Structured note-taking | nb, zk | [docs/06-note-taking.md](docs/06-note-taking.md) |
| Converts your writing to PDF/Word/HTML | pandoc | [docs/07-writing-and-publishing.md](docs/07-writing-and-publishing.md) |

---

## Frequently Asked Questions

**Do I need to know how to code?**
No. You just type the commands shown above. If you can copy and paste, you can use this.

**What if I already have papers saved as PDFs?**
Drop them in the `sources/` folder. Then use `make add-pdf PDF="sources/filename.pdf"` to add each one to your organized library.

**Can I collaborate with someone?**
Yes. Since this is a GitHub repository, multiple people can work on the same project. Each person forks or clones the repo and can push their changes.

**What if something breaks?**
Run `make check` to see which tools are installed and working. If something is missing, run `./setup.sh` again.

**Can I use this for a book, dissertation, or thesis?**
Absolutely. The structure works for any length of scholarly writing. Add more section files in `manuscript/` if you prefer to write chapters separately.

**I prefer Word/Google Docs for writing. Can I still use the other tools?**
Yes. You can use the search, download, note-taking, and reference management commands without writing in Markdown. When you're ready, export your bibliography with `make bib` and import the `.bib` file into your word processor's citation manager.

---

## Contributing

See [CONTRIBUTING.md](CONTRIBUTING.md). Suggestions, new tools, and improvements are welcome.

## License

MIT — see [LICENSE](LICENSE). Use it however you like.
