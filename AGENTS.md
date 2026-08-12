# Repository Guidelines

## Project Structure & Module Organization

This repository is a Python 3.11+ lab for evaluating a retrieval-augmented generation (RAG) assistant. Implement the reusable evaluation core in `template.py`, then copy the finished version to `solution/solution.py`; the tests prefer that file when it exists. `domain_assistant.py` retrieves from the Markdown corpus in `data/student_services/` and generates answers. `validate_golden_dataset.py` checks `golden_dataset.json`, while `evaluate_answers.py` scores saved responses. Tests live in `tests/test_solution.py`. Record lab conclusions in `exercises.md` and `reflection.md`. Generated JSON belongs under `artifacts/`.

## Build, Test, and Development Commands

Run commands from the repository root:

```powershell
python -m venv .venv
.\.venv\Scripts\Activate.ps1
python -m pip install -r requirements.txt
pytest tests/ -v
python validate_golden_dataset.py
python domain_assistant.py
python evaluate_answers.py
```

The first three commands create the environment and install dependencies. `pytest` runs the 42-test core suite. Dataset validation must report `PASS` before inference. The final two commands create `artifacts/actual_answers.json` and `artifacts/benchmark_results.json`; inference requires a configured API key.

## Coding Style & Naming Conventions

Use four-space indentation, UTF-8 files, type hints, and short docstrings for non-obvious behavior. Follow existing Python conventions: `snake_case` for functions and variables, `PascalCase` for classes, and `UPPER_CASE` for constants. Keep evaluation logic in the core module and artifact I/O in scripts. No formatter or linter is configured, so match the surrounding PEP 8-style code and avoid unrelated formatting changes.

## Testing Guidelines

Tests use `pytest` with `unittest`-style classes. Name new files `test_*.py`, classes `TestFeature`, and methods `test_expected_behavior`. Run a focused case while developing, for example:

```powershell
pytest tests/test_solution.py::TestLLMJudge -v
```

Before submission, run the complete suite and dataset validator. Remember that changes to `template.py` are ignored by tests after `solution/solution.py` exists unless you sync the files.

## Commit & Pull Request Guidelines

History is brief; the newest commit uses a Conventional Commit prefix (`feat:`). Prefer concise, imperative messages such as `fix: handle empty retrieval contexts`. Pull requests should summarize behavior changes, identify affected lab tasks, and include test and validation results. Link relevant issues and include sample output when benchmark reports change; screenshots are unnecessary for this CLI project.

## Security & Configuration

Copy `.env.example` to `.env` and set `OPENAI_API_KEY` and `OPENAI_MODEL`. Never commit `.env`, credentials, or externally supplied instructor data. Treat generated model answers as variable outputs, not secrets or deterministic fixtures.
