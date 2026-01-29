
# 🧭 uv – Practical Reference (Beginner → Company Workflow)

This document is a **future reference** for using `uv` correctly in a company-style Python project.

---

## 🧱 What is `uv`?

`uv` is:
- A **Python package manager**
- A **project manager**
- A **virtual environment manager**
- A **Python version manager**

It replaces:
- `pip`
- `python -m venv`
- `pip-tools`
- parts of Poetry

---

## 📁 Creating a New Project

### 1️⃣ Initialize a project
```bash
uv init my_project
cd my_project
````

Creates:

* `pyproject.toml`
* `.python-version`
* `README.md`
* basic structure

---

### 2️⃣ Set / change Python version

Edit `.python-version`:

```text
3.10
```

Then run:

```bash
uv sync
```

This recreates `.venv` with the correct Python version.

---

## 🐍 Virtual Environment

### 3️⃣ Create `.venv`

```bash
uv venv
```

or (recommended):

```bash
uv sync
```

> ⚠️ No need to activate `.venv`

---

## 📦 Dependency Management

### 4️⃣ Add production dependency

```bash
uv add requests
```

This:

* Installs the package
* Updates `pyproject.toml`
* Updates `uv.lock`

---

### 5️⃣ Add development-only dependency

```bash
uv add --dev ipykernel pytest jupyter
```

Use this for:

* notebooks
* testing
* linting
* formatting

---

## ▶️ Running Code

### 6️⃣ Run a Python file (recommended)

```bash
uv run python filename.py
```

✔ Uses correct `.venv`
✔ Uses correct Python version
✔ Works without activation
✔ Same behavior as CI

---

### 7️⃣ Run tests

```bash
uv run pytest
```

---

## 🔁 Syncing Environments

### 8️⃣ Install everything (dev + prod)

```bash
uv sync
```

Used for:

* local development
* onboarding
* normal work

---

### 9️⃣ Install ONLY production dependencies

```bash
uv sync --no-dev
```

Used for:

* deployment
* Docker
* production servers

---

## 🗑️ Resetting the Environment (Very Important)

If things behave strangely:

```bash
rmdir /s /q .venv
uv sync
```

`.venv` is disposable — **always safe to delete**.

---

## 📄 Important Files (What & Why)

### `pyproject.toml`

* Project definition
* Declares dependencies
* Declares Python version range
* **You edit this**

---

### `uv.lock`

* Exact dependency versions
* Used by CI and production
* **DO NOT edit manually**

---

### `.python-version`

* Declares Python version for project
* Used by `uv` and CI

---

### `.venv/`

* Virtual environment
* Contains Python + packages
* **Never commit**
* Safe to delete

---

### `src/`

* Real application code
* Import-safe structure

---

### `notebooks/`

* Experiments only
* No production logic

---

## ✅ DOs (Company Best Practices)

✔ Use `uv run` instead of raw `python`
✔ Use `uv add` / `uv add --dev`
✔ Keep `.python-version`
✔ Delete & recreate `.venv` when unsure
✔ Move real logic into `src/`
✔ Run tests before pushing
✔ Trust `uv.lock`

---

## ❌ DON’Ts (Common Mistakes)

❌ `pip install` manually
❌ `!pip install` inside notebooks
❌ Edit `uv.lock` by hand
❌ Commit `.venv`
❌ Rely on activated environments
❌ Share environments across projects
❌ Put all logic in notebooks

---

## 🧠 Mental Models to Remember

* **Project controls Python, not your laptop**
* **If it’s not in `pyproject.toml`, it doesn’t exist**
* **`.venv` is cattle, not a pet**
* **CI runs what you run with `uv run`**

---

## 🧪 Notebook Usage (Safe Way)

```bash
uv add --dev ipykernel jupyter
uv run jupyter lab
```

OR simply:

* Create `.ipynb` in VS Code
* Select `.venv` kernel
* Never install packages inside notebook

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

## 🎯 Final Note

You do NOT need to memorize everything.

If stuck:

```bash
uv sync
uv run pytest
```

If still stuck:

```bash
rmdir /s /q .venv
uv sync
```

This fixes most issues.



