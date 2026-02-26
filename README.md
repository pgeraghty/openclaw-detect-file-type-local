# detect-file-type-local

[![CI](https://github.com/pgeraghty/openclaw-detect-file-type-local/actions/workflows/ci.yml/badge.svg?branch=main)](https://github.com/pgeraghty/openclaw-detect-file-type-local/actions/workflows/ci.yml)
[![License: MIT](https://img.shields.io/github/license/pgeraghty/openclaw-detect-file-type-local)](LICENSE)
![PyPI](https://img.shields.io/pypi/v/detect-file-type-local)
![Python 3.8+](https://img.shields.io/badge/python-3.8%2B-blue)
![Inference: Local/Offline](https://img.shields.io/badge/inference-local%20%7C%20offline-success)
![API Keys](https://img.shields.io/badge/api_keys-none-success)

An [OpenClaw](https://openclaw.org) skill for AI-powered local file type detection.

Wraps [Google Magika](https://github.com/google/magika) to provide ML-based file type identification that runs entirely offline. No API keys, no network calls — just local inference on an embedded ONNX model.

## Features

- **214 file types** detected by content, not extension
- **Fully offline** — no network access required
- **Fast** — only reads the bytes needed for classification
- **Batch support** — process multiple files or entire directories
- **Multiple output formats** — JSON, human-readable, bare MIME type
- **Stdin support** — pipe content directly

## Quick Start

```bash
pip install detect-file-type-local

# Detect a single file
detect-file-type-local document.pdf

# Batch detect
detect-file-type-local --human *.pdf *.png

# Recursive directory scan
detect-file-type-local -r ./uploads/

# Pipe from stdin
cat mystery_file | detect-file-type-local -
```

Compatibility alias: `detect-file-type` remains available.

## Output Formats

**JSON (default):**
```json
{
  "path": "photo.jpg",
  "label": "jpeg",
  "mime_type": "image/jpeg",
  "score": 0.99,
  "group": "image",
  "description": "JPEG image",
  "is_text": false
}
```

**Human-readable:**
```
photo.jpg: JPEG image (image/jpeg) [score: 0.99]
```

**MIME-only:**
```
image/jpeg
```

## OpenClaw Skill

See [SKILL.md](SKILL.md) for the OpenClaw skill definition, including structured output schemas and usage guidance for LLM integration.

OpenClaw skill metadata now auto-installs from PyPI package `detect-file-type-local`.

## Development

```bash
pip install -e '.[dev]'
pytest tests/ -v
ruff check .
```

## Release

PyPI publishing is automated via GitHub Actions (`Publish Python Package` workflow):

1. Create a GitHub release with a tag matching package version (for example, `v0.1.0`)
2. Workflow builds and validates artifacts
3. Workflow publishes to PyPI via trusted publishing

After PyPI release, update and republish the ClawHub skill metadata to enable auto-install from `detect-file-type-local`.

## License

MIT — see [LICENSE](LICENSE).

This project uses [Google Magika](https://github.com/google/magika) (Apache-2.0). See [NOTICE](NOTICE) and [THIRD_PARTY_LICENSES.md](THIRD_PARTY_LICENSES.md).
