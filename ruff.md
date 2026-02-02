
# 🦅 Ruff – Python Linting & Formatting (Beginner → Company Guide)

This document explains what **Ruff** is, why companies use it,
and how to use it safely with `uv`.

---

## 🔧 What is Ruff?

**Ruff** is a **Python linter and formatter**.

In simple words:
> Ruff checks your Python code for mistakes, bad practices,
> and style issues — and can fix many of them automatically.

Ruff is:
- ⚡ Extremely fast (written in Rust)
- 🧠 Very strict (in a good way)
- 🏢 Widely used in modern Python companies

---

## 🧠 What Problems Does Ruff Solve?

Python allows many things that are **technically valid** but **bad practice**.

Examples:
- Unused imports
- Unused variables
- Inconsistent formatting
- Common bug patterns
- Messy diffs in code reviews

Ruff catches these **before humans need to**.

---

## ❓ Is Ruff Required to Run Python Code?

❌ No — your code runs without Ruff.

✅ But in companies:
- CI often runs Ruff
- Pull requests fail if Ruff fails
- Code quality is enforced automatically

Think of Ruff as:
> **Spell-check + grammar-check for Python**

---

## 📦 Installing Ruff (Development Only)

Ruff is a **development dependency**.

```bash
uv add --dev ruff
````

Why dev-only?

* Not needed in production
* Only used by developers & CI

---

## ▶️ Running Ruff

### Check code (no changes)

```bash
uv run ruff check .
```

This:

* Scans all Python files
* Reports problems
* Does NOT modify code

---

### Auto-fix safe issues

```bash
uv run ruff check . --fix
```

This can automatically:

* Remove unused imports
* Fix formatting issues
* Apply safe code improvements

---

## 🧪 Example (Before & After)

### Before Ruff

```python
import os

def add(a,b):
    return a+b
```

### After `ruff --fix`

```python
def add(a, b):
    return a + b
```

Clean, consistent, professional.

---

## 🧠 Ruff vs Tests (Important)

| Tool     | Purpose               |
| -------- | --------------------- |
| `pytest` | Verifies correctness  |
| `ruff`   | Enforces code quality |

You need **both**.

---

## 🤖 Ruff in CI

CI commonly runs:

```bash
uv run ruff check .
uv run pytest
```

If Ruff fails:

* ❌ CI fails
* ❌ Code cannot be merged

This keeps code quality high.

---

## 📄 Basic Ruff Configuration (Optional)

Ruff is usually configured in `pyproject.toml`.

Example:

```toml
[tool.ruff]
line-length = 88
target-version = "py310"
```

⚠️ Do NOT overconfigure as a beginner.

---

## ❌ Common Beginner Mistakes

❌ Ignoring Ruff errors
❌ Editing `uv.lock` to fix Ruff
❌ Disabling Ruff rules randomly
❌ Running Ruff outside `uv`

---

## ✅ Best Practices

✔ Run Ruff before committing
✔ Use `--fix` for safe auto-fixes
✔ Let CI enforce Ruff
✔ Ask before disabling rules

---

## 🧠 Mental Model (Remember This)

> **Ruff is a fast, strict reviewer that never gets tired.**

It saves time, avoids nitpicks, and improves code quality.

---

## 🧭 Typical Workflow

```bash
uv run ruff check .
uv run ruff check . --fix
uv run pytest
```

---

## 🎯 Final Takeaway

* Ruff does NOT make code slower
* Ruff does NOT change logic
* Ruff makes code readable, consistent, and safe

If Ruff complains, **it’s helping you**.


