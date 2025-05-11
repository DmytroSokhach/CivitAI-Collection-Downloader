# Changelog

## [Unreleased]

### Added
- (2025-05-11) Medium: Support for filtering collection downloads by query params (e.g., `baseModels=Illustrious&withMeta=true&tools=86`).
    - `api.py`: `get_images_in_collection` and `get_all_images_in_collection` accept a `filters` dict.
    - `main.py`: New `--filter` CLI argument, parsed and passed to API.
    - `README.md`: Documented new feature and usage example.

### Changed
- None

### Fixed
- None
