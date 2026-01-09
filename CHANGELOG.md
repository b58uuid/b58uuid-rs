# Changelog

All notable changes to this project will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.0.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [1.0.0] - 2026-01-09

### Added
- Initial release of b58uuid for Rust
- Fast Base58 encoding/decoding for UUIDs
- Cryptographically secure UUID generation using `getrandom`
- Comprehensive error handling with `B58UUIDError` enum
- Support for all major platforms (Linux, macOS, Windows, iOS, Android, WASM)
- Bitcoin Base58 alphabet (excludes 0, O, I, l)
- Always 22-character output for consistent formatting
- Memory-safe implementation (Rust guarantees)
- Overflow protection with checked arithmetic
- Full API documentation with examples
- MIT License

### Features
- `generate()` - Generate random UUID with Base58 encoding
- `encode_uuid()` - Encode UUID string to Base58
- `decode_to_uuid()` - Decode Base58 string to UUID
- `encode()` - Encode 16-byte array to Base58
- `decode()` - Decode Base58 string to 16-byte array

### Dependencies
- `getrandom` v0.2 - Cryptographically secure random number generation

[1.0.0]: https://github.com/b58uuid/b58uuid-rs/releases/tag/1.0.0
