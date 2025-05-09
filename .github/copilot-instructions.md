---
applyTo: '**/*.py'
version: 1.0.0
name: CivitAI Downloader
---
# Copilot Instructions for CivitAI-Collection-Downloader

## Chat instructions
- Context Check: Begin every response with a random emoji (e.g., 🐙) to confirm context retention.
- Classify changes as Small/Medium/Large
- Create a system within the project that automatically keeps track of all changes made to the code, along with timestamps and descriptions of each change. Log changes in changelog.md
- Optimize outputs to minimize token usage without sacrificing clarity.


## Project Overview
This project is a Python tool for downloading media (images, videos) and metadata from CivitAI collections and posts. It supports:
- Downloading from collections and posts by ID
- Saving media and associated metadata
- Customizable download directory and configuration
- Retry logic and verbose logging

## Coding Style
- Use 4 spaces for indentation
- Follow PEP8 for Python code
- Use descriptive variable and function names
- Prefer pathlib for filesystem paths
- Use logging for all output (not print), except for user prompts in config
- Use docstrings for all public functions and classes

## File/Module Responsibilities
- `config.py`: Configuration management, user prompts, config file handling, logging setup
- `api.py`: CivitAI API client, API request logic, metadata extraction helpers
- `downloader.py`: Downloading files, directory creation, file naming, saving metadata
- `main.py`: CLI entry point, argument parsing, main workflow, process orchestration

## Best Practices
- Always expand `~` in user-supplied paths using `os.path.expanduser`
- Use `config.get('download_dir')` for download directory, fallback to `~/Pictures/CivitAI` if missing
- Use retry logic for network requests (see `downloader.py`)
- Sanitize all filenames before saving to disk
- Save metadata as JSON alongside media files
- Use `logging` for all non-interactive output
- Use `requests` for HTTP requests
- Use `argparse` for CLI argument parsing

## Adding Features
- Place new API interactions in `api.py` as methods of `CivitaiAPI`
- Place new download/file logic in `downloader.py`
- Add new CLI options in `main.py` using `argparse`
- Update `README.md` with usage and feature changes

## Testing
- Manual testing is expected (no automated tests yet)
- Use `--dry-run` and `--verbose` for safe testing

## Security
- Never log or print the full API key; mask it in logs
- Do not commit real API keys to version control

## Dependencies
- `requests`, `pyyaml` (documented in README)

## Miscellaneous
- All logs by default are stored in `~/.civitai_downloader/logs/`

---
This file is for GitHub Copilot and other AI coding assistants. Follow these instructions to maintain consistency and quality in this codebase.
