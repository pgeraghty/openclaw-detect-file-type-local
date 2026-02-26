# detect-file-type-local

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
pip install -e .

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

Note: this skill currently uses manual local installation (`pip install -e ...`). Auto-install metadata will be added after a public package artifact is published and resolvable.

## Development

```bash
pip install -e '.[dev]'
pytest tests/ -v
ruff check .
```

## License

MIT — see [LICENSE](LICENSE).

This project uses [Google Magika](https://github.com/google/magika) (Apache-2.0). See [NOTICE](NOTICE) and [THIRD_PARTY_LICENSES.md](THIRD_PARTY_LICENSES.md).
