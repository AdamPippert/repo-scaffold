# repo‑scaffold

`repo‑scaffold` is a **one‑file automation kit** that converts an ASCII‑tree
directory diagram into a fully initialised Git repository—complete with all
folders, placeholder files, a `.gitignore`, and a Markdown copy of the original
scaffold for traceability.

The project contains only two artifacts:

| Path                   | Purpose                                   |
| ---------------------- | ----------------------------------------- |
| `generate_scaffold.sh` | Bash script that builds the repository.   |
| `README.md`            | The document you are reading now.         |

---

## 1. Why you might want this

* **Lightning‑fast bootstraps** for workshops, demos, or hack‑day projects
  from an LLM request or a collaborative brainstorming session  
* **Exact parity** between the diagram you agreed upon and the directory that
  lands on disk—no missing files, no typos  
* **Self‑documenting**: the ASCII tree is stored under `specs/structure.md`
  inside the new repo so future contributors know the intended layout  

---

## 2. Prerequisites

| Tool | Tested Versions |
| ---- | --------------- |
| **Bash** | 4.x or 5.x |
| **GNU coreutils** | Standard on most Linux distributions and macOS (via Homebrew) |
| **Git** | 2.20 or newer |

The script is POSIX‑friendly but requires Bash‑style arrays, so `sh` alone will
_not_ work.

---

## 3. Quick Start

```bash
# 1. Clone this helper repo
git clone https://github.com/AdamPippert/repo-scaffold.git
cd repo-scaffold

# 2. Make the script executable
chmod +x generate_scaffold.sh

# 3. Prepare (or paste) your scaffold into a file
cat > scaffold.txt <<'TREE'
.
├── README.md            # Project overview
├── .gitignore           # Excludes .env, build/
├── src/
│   ├── main.py
│   └── utils.py
└── build/               # git-ignored
TREE

# 4. Create an empty working directory for the new project
mkdir ../my-new-project && cd ../my-new-project

# 5. Run the generator, feeding it the scaffold text
../repo-scaffold/generate_scaffold.sh ../repo-scaffold/scaffold.txt
