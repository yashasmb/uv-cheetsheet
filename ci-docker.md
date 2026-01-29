# 🐳 Docker + CI with `uv` (Practical & Beginner-Friendly)

This section explains:
- Why Docker is used
- How `uv` fits into Docker
- How CI uses `uv`
- What juniors are expected to understand (and what not)

---

## 🧠 What is Docker (in simple words)?

Docker creates a **clean, isolated machine** for your project.

Think of Docker as:
> “A fresh laptop that starts from zero every time”

Why companies use it:
- Same behavior on every machine
- Same behavior in CI
- Same behavior in production

---

## 🔑 Important Mental Model

> **CI ≈ Docker ≈ Clean Machine**

Both:
- Do NOT reuse your local `.venv`
- Do NOT rely on your laptop
- Recreate everything from scratch

That’s why `uv` + lockfiles matter.

---

## 🧱 How `uv` fits into Docker

Inside Docker:
- No Python is assumed
- No dependencies are assumed
- No `.venv` exists

So Docker does:
```bash
uv sync --no-dev
````

And `uv` handles:

* Python version
* Virtual environment
* Exact dependencies

---

## 🐳 Example: Minimal Dockerfile (Production)

```dockerfile
FROM debian:bookworm-slim

# Install system dependencies
RUN apt-get update && apt-get install -y curl ca-certificates

# Install uv
RUN curl -LsSf https://astral.sh/uv/install.sh | sh

WORKDIR /app

# Copy project files
COPY pyproject.toml uv.lock .python-version ./
COPY src ./src

# Install production dependencies only
RUN uv sync --no-dev

# Run the app
CMD ["uv", "run", "python", "src/my_project/main.py"]
```

### What this Dockerfile guarantees

✔ Correct Python version
✔ Exact dependency versions
✔ No dev tools in production
✔ Same behavior as CI

---

## ❗ Important Docker Rules

### ✅ DO

* Use `uv sync --no-dev`
* Copy `pyproject.toml` + `uv.lock`
* Let `uv` manage Python

### ❌ DON’T

* `pip install` in Docker
* Copy `.venv` into Docker
* Rely on system Python

---

## 🤖 What is CI (Continuous Integration)?

CI is:

> **An automated robot that runs your project on every push**

CI usually does:

1. Create a clean machine
2. Clone your repo
3. Install dependencies
4. Run tests
5. Report success or failure

---

## 🧠 Why CI always works when local works (if done right)

Because CI runs:

```bash
uv sync
uv run pytest
```

Exactly what you run locally.

---

## 🧪 Example: GitHub Actions CI (Beginner Safe)

```yaml
name: Python CI

on: [push, pull_request]

jobs:
  test:
    runs-on: ubuntu-latest

    steps:
      - uses: actions/checkout@v4

      - name: Install uv
        run: |
          curl -LsSf https://astral.sh/uv/install.sh | sh

      - name: Sync dependencies
        run: uv sync

      - name: Run tests
        run: uv run pytest
```

---

## 🧠 What CI checks (and what it doesn’t)

### CI checks:

✔ Code correctness
✔ Dependency correctness
✔ Test results
✔ Python version

### CI does NOT care about:

❌ Your local `.venv`
❌ Your VS Code setup
❌ Your shell state

---

## 🔁 Dev vs CI vs Production (Very Important Table)

| Environment | Command Used       |
| ----------- | ------------------ |
| Local dev   | `uv sync`          |
| CI          | `uv sync`          |
| Production  | `uv sync --no-dev` |

Same tool. Same rules. Different scope.

---

## 🧨 Common CI Failures (and what they mean)

### ❌ “Module not found”

➡ Dependency not added via `uv add`

### ❌ “Python version mismatch”

➡ `.python-version` or `requires-python` incorrect

### ❌ “Works locally, fails in CI”

➡ Local `.venv` is dirty → recreate it

Fix:

```bash
rm -rf .venv
uv sync
```

---

## ✅ What Juniors Are Expected to Know

✔ How to read CI errors
✔ How to run the same commands locally
✔ How to fix dependency issues
✔ When to delete `.venv`

❌ NOT expected:

* Writing CI from scratch
* Optimizing Docker images
* Managing CI infrastructure

---

## 🧠 Final Mental Model (Remember This)

> **If it works with `uv run`, it works in CI and Docker**

That’s the goal.

---

## 🧭 Debugging Checklist (CI / Docker Issues)

```bash
uv run python --version
uv sync
uv run pytest
```

If still broken:

```bash
rm -rf .venv
uv sync
```

---

## 🎯 Final Takeaway

* Docker = clean machine
* CI = automated clean machine
* `uv` = the bridge that makes them painless

If you trust `uv` and the lockfile,
everything else becomes predictable.


