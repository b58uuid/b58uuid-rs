# B58UUID for Rust

[![Crates.io](https://img.shields.io/crates/v/b58uuid.svg)](https://crates.io/crates/b58uuid)
[![Documentation](https://docs.rs/b58uuid/badge.svg)](https://docs.rs/b58uuid)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![Build Status](https://github.com/b58uuid/b58uuid-rs/workflows/Tests/badge.svg)](https://github.com/b58uuid/b58uuid-rs/actions)
[![Downloads](https://img.shields.io/crates/d/b58uuid.svg)](https://crates.io/crates/b58uuid)

Base58-encoded UUID library for Rust with minimal dependencies.

## Why This Library?

- **Compact**: 22 characters instead of 36
- **URL-safe**: No special characters that need escaping
- **Unambiguous**: Uses Bitcoin's Base58 alphabet (excludes 0, O, I, l)
- **Fast**: Optimized encoding/decoding with lookup tables
- **Safe**: Memory-safe by design (Rust guarantees)
- **Cross-platform**: Works on Linux, macOS, Windows, iOS, Android, WASM

## Installation

Add to your `Cargo.toml`:

```toml
[dependencies]
b58uuid = "1.0"
```

## Usage

```rust
use b58uuid;

fn main() -> Result<(), Box<dyn std::error::Error>> {
    // Generate a new UUID
    let b58 = b58uuid::generate();
    println!("{}", b58); // Output: 3FfGK34vwMvVFDedyb2nkf

    // Encode existing UUID
    let encoded = b58uuid::encode_uuid("550e8400-e29b-41d4-a716-446655440000")?;
    println!("{}", encoded); // Output: BWBeN28Vb7cMEx7Ym8AUzs

    // Decode back to UUID
    let uuid = b58uuid::decode_to_uuid("BWBeN28Vb7cMEx7Ym8AUzs")?;
    println!("{}", uuid); // Output: 550e8400-e29b-41d4-a716-446655440000

    Ok(())
}
```

## API

### Functions

- `generate() -> String` - Generate a new random UUID and return Base58 encoding
- `encode_uuid(uuid_str: &str) -> Result<String, B58UUIDError>` - Encode UUID string to Base58
- `decode_to_uuid(b58_str: &str) -> Result<String, B58UUIDError>` - Decode Base58 string to UUID
- `encode(data: &[u8; 16]) -> String` - Encode 16-byte array to Base58
- `decode(b58_str: &str) -> Result<[u8; 16], B58UUIDError>` - Decode Base58 string to 16-byte array

### Error Type

`B58UUIDError` enum with variants:
- `InvalidUUID(String)` - Invalid UUID format
- `InvalidBase58(String)` - Invalid Base58 string
- `InvalidLength { expected: usize, got: usize }` - Invalid length
- `Overflow` - Arithmetic overflow during conversion

## Features

- **Minimal dependencies**: Only uses `getrandom` for secure random number generation
- **Always 22 characters**: Consistent, predictable output length
- **Bitcoin Base58 alphabet**: No confusing characters (0, O, I, l)
- **Memory safe**: Rust's compile-time guarantees prevent common bugs
- **Full error handling**: All operations return `Result` types
- **Cross-platform**: Works on all major platforms including embedded systems

## Dependencies

This library has only **one dependency**: [`getrandom`](https://crates.io/crates/getrandom)

### Why `getrandom`?

Rust's standard library intentionally does not provide cryptographically secure random number generation. The `getrandom` crate is the de facto standard solution in the Rust ecosystem for this purpose.

**Benefits of using `getrandom`**:
- ✅ **Cryptographically secure** on all platforms (Linux, macOS, Windows, iOS, Android, WASM)
- ✅ **Minimal overhead**: Small, well-audited crate with no transitive dependencies
- ✅ **Widely trusted**: Used by the `rand` crate and thousands of other projects
- ✅ **Platform abstraction**: Automatically uses the best random source for each platform:
  - Linux: `getrandom()` syscall
  - macOS/BSD: `/dev/urandom`
  - Windows: `BCryptGenRandom()`
  - WASM: `crypto.getRandomValues()`

Without `getrandom`, we would need to manually implement platform-specific code for each operating system, which would be error-prone and harder to maintain.

## Testing

```bash
cargo test
```

## License

MIT License - see LICENSE file for details.
