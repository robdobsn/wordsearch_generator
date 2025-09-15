ns # Build Instructions

## Windows Build Requirements

To compile this Rust project on Windows, you need:

1. **Rust toolchain** (already installed)
2. **Visual Studio Build Tools** or **Visual Studio Community** with C++ support

### Installing Visual Studio Build Tools

1. Download Visual Studio Installer from: https://visualstudio.microsoft.com/downloads/
2. Install "Build Tools for Visual Studio 2022" (free)
3. In the installer, select:
   - Workloads: "C++ build tools"
   - Individual components: "MSVC v143 - VS 2022 C++ x64/x86 build tools"
   - Individual components: "Windows 10 SDK" (latest version)

### Alternative: Use WSL or Linux

If you prefer to avoid Windows-specific build tools:

1. Install WSL2 with Ubuntu
2. Install Rust in WSL: `curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh`
3. Build the project in WSL: `cargo build --release`

### After Installing Build Tools

Once the build tools are installed, you can:

```bash
# Build the project
cargo build --release

# Run with example data
cargo run --release -- --input example_words.yaml

# Run without progress output
cargo run --release -- --input example_words.yaml --silent
```

## Demo Version

A Python demo (`demo.py`) is provided to show the algorithm working without compilation requirements.
