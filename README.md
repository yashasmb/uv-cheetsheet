# 🧭 uv – Complete Python Project Reference

## 🔧 What is `uv`?

`uv` is a modern tool that replaces:
- `pip`
- `python -m venv`
- `pip-tools`
- parts of Poetry

It handles:
- Python version management
- Virtual environments
- Dependency installation
- Lockfile generation
- Running commands safely

---

## 🐍 Do I Need Python Installed on My Laptop?

> ❌ **No. `uv` manages Python for you.**

- `uv` downloads and stores Python versions automatically
- Each project uses its own isolated Python
- System Python is never touched

**Company-safe rule:**
✔ Let `uv` manage Python
✔ Never rely on system Python
✔ Python version is a **project concern**, not a laptop concern

---

## 🛠️ Installing `uv`

**Windows (PowerShell):**
```powershell
irm https://astral.sh/uv/install.ps1 | iex
```

**macOS / Linux:**
```bash
curl -LsSf https://astral.sh/uv/install.sh | sh
```

**Verify:**
```bash
uv --version
```

---

## 📁 Creating a New Project

```bash
uv init my_project
cd my_project
```

Or with a specific Python version:
```bash
uv init my_project --python 3.11
```

Creates:
- `pyproject.toml`
- `.python-version`
- `README.md`

---

## 🐍 Virtual Environment

```bash
uv sync
```

This:
- Downloads correct Python (if needed)
- Creates `.venv`
- Installs all dependencies

> ⚠️ No need to activate `.venv` — ever.

---

## 📦 Dependency Management

### Add a production dependency
```bash
uv add requests
```

### Add a dev-only dependency
```bash
uv add --dev pytest ipykernel jupyter ruff
```

Dev dependencies are for:
- Testing (`pytest`)
- Notebooks (`ipykernel`, `jupyter`)
- Linting / formatting (`ruff`)

### Remove a dependency
```bash
uv remove requests
```

### Upgrade a specific package
```bash
uv add requests --upgrade
```

### Upgrade all dependencies
```bash
uv lock --upgrade
uv sync
```

---

## ▶️ Running Code

### Run a Python file
```bash
uv run main.py
# or explicitly:
uv run python main.py
```

### Run tests
```bash
uv run pytest
```

### Run with a temporary package (no install needed)
```bash
uv run --with httpx python main.py
```
Useful for quick one-off scripts without polluting your project dependencies.

---

## 🔁 Syncing Dependencies

### Install everything (dev + prod) — use for local development
```bash
uv sync
```

### Install only production dependencies — use for Docker / CI / deployment
```bash
uv sync --no-dev
```

---

## 🗑️ Resetting the Environment

If things behave strangely, `.venv` is always safe to delete:

**Windows:**
```powershell
rmdir /s /q .venv
uv sync
```

**macOS / Linux:**
```bash
rm -rf .venv
uv sync
```

> `.venv` is cattle, not a pet. Delete it without guilt.

---

## 📄 Important Files

| File | Purpose | Edit? |
|---|---|---|
| `pyproject.toml` | Project metadata + dependencies | ✅ Yes |
| `uv.lock` | Exact locked versions for all deps | ❌ Never manually |
| `.python-version` | Python version for this project | ✅ Yes |
| `.venv/` | Local virtual environment | ❌ Never commit |

---

## 🗂️ Recommended Project Structure

```
my_project/
├── src/
│   └── my_project/
│       └── main.py       ← real application code
├── notebooks/            ← experiments only, no production logic
├── tests/
│   └── test_main.py
├── pyproject.toml
├── uv.lock
├── .python-version
└── README.md
```

> Put real logic in `src/`, not in notebooks.

---

## 🧪 Notebooks (Safe Usage)

```bash
uv add --dev ipykernel jupyter
uv run jupyter lab
```

Or in VS Code: open `.ipynb` and select the `.venv` kernel.

❌ Never `pip install` or `!pip install` inside a notebook cell.

---

## ✅ DOs

- ✔ Use `uv run` instead of raw `python`
- ✔ Use `uv add` / `uv add --dev` — never `pip install`
- ✔ Keep `.python-version` in version control
- ✔ Commit `uv.lock` — it's the source of truth for CI and production
- ✔ Delete `.venv` when something feels off
- ✔ Run tests before pushing

---

## ❌ DON'Ts

- ❌ `pip install` manually
- ❌ `!pip install` inside notebooks
- ❌ Edit `uv.lock` by hand
- ❌ Commit `.venv`
- ❌ Rely on system Python
- ❌ Share `.venv` across projects
- ❌ Put production logic in notebooks

---

## 🧠 Key Mental Models

- **Project controls Python, not your laptop**
- **If it's not in `pyproject.toml`, it doesn't exist**
- **`uv.lock` is the source of truth**
- **`.venv` is disposable — cattle, not a pet**
- **`uv run` = same behavior locally and in CI**

---

## 🧭 Daily Workflow

```bash
uv sync              # start of day / after pulling changes
uv run pytest        # before editing
# ...edit code...
uv run pytest        # after editing
git commit
git push
```

---

## 🚨 Troubleshooting

| Problem | Fix |
|---|---|
| Wrong Python version | Check `.python-version`, run `uv sync` |
| Package not found | `uv add <package>` |
| Weird environment state | `rm -rf .venv && uv sync` |
| Deps out of date | `uv lock --upgrade && uv sync` |
| CI fails but local works | Make sure `uv.lock` is committed |

---

## 🎯 If You're Stuck

```bash
uv sync
uv run pytest
```

Still stuck:
```bash
rm -rf .venv
uv sync
```
