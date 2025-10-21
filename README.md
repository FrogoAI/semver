### Go SemVer: A High-Performance, Regex-Free Semantic Versioning Parser

A lightweight, performant Go package for parsing and comparing semantic version strings. It is designed for systems where version precedence is critical and avoids the overhead of regular expressions by using direct string parsing.

This library converts version strings into a fixed-size, comparable integer (`*big.Int`) or hex representation, making sorting and comparison operations extremely fast and suitable for performance-sensitive applications.

### Core Features

- **Strict Parsing**: Validates version strings and rejects malformed inputs with specific errors (e.g., empty segments, leading zeros, invalid delimiters).
- **Regex-Free Design**: Implements a custom string-slicing parser for maximum performance and minimal overhead.
- **Comparable Binary Output**: Provides `Hex()` and `Num()` methods to get a fixed-size representation suitable for efficient database indexing, sorting, and direct comparison.
- **Pre-release Keyword Support**: Natively understands common pre-release keywords like `alpha`, `beta`, and `rc`, ensuring correct precedence (`1.0.0-rc.1` < `1.0.0`).

### Design and Limitations

To maintain simplicity and a fixed-size format, this package includes specific design choices:

- **Non-Standard Alphanumeric Handling**: Pre-release identifiers that are not numeric or a recognized keyword (e.g., "alpha") are handled by a **custom character-byte-sum algorithm**. This is **not compliant with SemVer's lexicographical sorting** but provides a deterministic way to compare them.
- **Build Metadata**: Build metadata (e.g., `+build.123`) is parsed but **ignored** in the final binary representation, strictly adhering to the SemVer 2.0.0 specification for precedence comparison.
