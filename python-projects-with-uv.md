
# 🐍 Python Projects with `uv` – Complete Beginner → Company Guide

This document explains how to create, run, and maintain Python projects
using `uv` in a **company-friendly, reproducible way**.

This is written for:
- Freshers
- New joiners
- Anyone confused by environments, Python versions, or CI

---

## 🔧 What is `uv`?

`uv` is a modern tool that:
- Manages Python versions
- Creates virtual environments
- Installs dependencies
- Locks exact versions
- Runs commands safely

It replaces:
- `pip`
- `python -m venv`
- `pip-tools`
- parts of Poetry

---

## 🧩 Do I Need Python Installed on My Laptop?

### Short answer
> ❌ **No, you do NOT need to install Python manually**

`uv` can:
- Download Python automatically
- Manage multiple versions
- Keep them isolated per project

### When Python IS needed
- To run `uv` itself (bundled or auto-managed)
- For legacy tools not using `uv`

### Recommendation (company-safe)
✔ Let `uv` manage Python  
✔ Do NOT depend on system Python  
✔ Do NOT switch Python versions manually  

> **Python version is a project concern, not a laptop concern**

---

## 🛠️ Installing `uv`

### Windows (PowerShell)
```powershell
irm https://astral.sh/uv/install.ps1 | iex
````

### macOS / Linux

```bash
curl -LsSf https://astral.sh/uv/install.sh | sh
```

Verify installation:

```bash
uv --version
```

---

## 📁 Creating a New Project

### 1️⃣ Initialize project

```bash
uv init my_project
cd my_project
```

Creates:

* `pyproject.toml`
* `.python-version`
* `README.md`

---

### 2️⃣ Set Python version

Edit `.python-version`:

```text
3.10
```

Or at creation time:

```bash
uv init my_project --python 3.10
```

---

## 🐍 Virtual Environment

### 3️⃣ Create environment (recommended)

```bash
uv sync
```

This:

* Downloads correct Python
* Creates `.venv`
* Installs dependencies

> ⚠️ No activation required

---

## 📦 Dependency Management

### 4️⃣ Add production dependency

```bash
uv add requests
```

Updates:

* `pyproject.toml`
* `uv.lock`

---

### 5️⃣ Add development-only dependency

```bash
uv add --dev pytest ipykernel jupyter
```

Used for:

* testing
* notebooks
* linting
* formatting

---

## ▶️ Running Code

### 6️⃣ Run Python file

```bash
uv run python filename.py
```

✔ Correct Python
✔ Correct `.venv`
✔ Same behavior as CI

---

### 7️⃣ Run tests

```bash
uv run pytest
```

---

## 🔁 Syncing Dependencies

### 8️⃣ Install all dependencies

```bash
uv sync
```

Used for:

* development
* onboarding

---

### 9️⃣ Install only production dependencies

```bash
uv sync --no-dev
```

Used for:

* deployment
* Docker
* production servers

---

## 🗑️ Resetting Environment (Safe & Common)

If anything breaks:

```bash
rmdir /s /q .venv   # Windows
rm -rf .venv        # macOS / Linux

uv sync
```

`.venv` is disposable.

---

## 📄 Important Files Explained

### `pyproject.toml`

* Project metadata
* Declares dependencies
* Declares Python compatibility
* **Editable by humans**

---

### `uv.lock`

* Exact versions of all dependencies
* Used by CI & production
* **DO NOT edit manually**

---

### `.python-version`

* Project Python version
* Used by `uv` and CI

---

### `.venv/`

* Isolated environment
* Never committed
* Safe to delete

---

### `src/`

* Application source code
* Prevents import bugs

---

### `notebooks/`

* Experiments only
* No production logic

---

## 🧪 Notebooks (Safe Usage)

```bash
uv add --dev ipykernel jupyter
uv run jupyter lab
```

OR use VS Code notebooks with `.venv` kernel.

❌ Never `pip install` inside notebooks.

---

## ✅ DOs (Best Practices)

✔ Use `uv run`

✔ Use `uv add` / `uv add --dev`

✔ Keep `.python-version`

✔ Delete `.venv` when unsure

✔ Run tests before pushing

✔ Trust `uv.lock`

---

## ❌ DON’Ts (Common Mistakes)

❌ `pip install` manually

❌ Edit `uv.lock`

❌ Commit `.venv`

❌ Put logic only in notebooks

❌ Rely on activated environments

---

## 🧠 Key Mental Models

* Project controls Python, not your laptop
* Lockfile is the source of truth
* `.venv` is disposable
* CI runs the same commands you do

---

## 🧭 Typical Daily Workflow

```bash
uv sync
uv run pytest
edit code
uv run pytest
commit
push
```

---

## 🎯 Final Notes

If stuck:

```bash
uv sync
uv run pytest
```

If still stuck:

```bash
rm -rf .venv
uv sync
```

This fixes most issues.

---


# Part 2️⃣ — **Do I Need Python Installed on My Laptop? (Final Answer)**

### 🔑 The truth (no ambiguity)

> **You can work entirely with `uv` without installing Python manually.**

### What actually happens
- `uv` downloads Python versions when needed
- Stores them safely
- Uses them per project
- Does NOT touch system Python

### Why companies prefer this
- No version conflicts
- Identical dev & CI environments
- Easy onboarding

### When having system Python is okay
- Legacy projects
- Scripts outside `uv`
- Learning basics (optional)

### Company-safe recommendation
✔ Let `uv` manage Python  
✔ Avoid relying on system Python  
✔ Treat Python like a project dependency  

