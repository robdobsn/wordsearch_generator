# Word Search Generator - WSL2 Setup Guide

This guide will get the word search generator running in WSL2 from scratch.

## Step 1: Install Rust in WSL2

```bash
# Install Rust
curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh

# Source the environment
source ~/.bashrc

# Verify installation
rustc --version
cargo --version
```

## Step 2: Copy Project Files

If you're working in Cursor with WSL2, the files should already be accessible. Otherwise:

```bash
# Navigate to your project directory
cd /mnt/c/Users/rob/Documents/rdev/WordSearchCreation/wordsearch_generator

# Or copy files to WSL home if needed
cp -r /mnt/c/Users/rob/Documents/rdev/WordSearchCreation/wordsearch_generator ~/
cd ~/wordsearch_generator
```

## Step 3: Build and Test

```bash
# Build the project (should work without MSVC issues)
cargo build --release

# Test with the example
cargo run --release -- --input example_words.yaml

# Test with silent mode
cargo run --release -- --input example_words.yaml --silent

# Test with small example
cargo run --release -- --input small_example.yaml
```

## Step 4: Expected Output

You should see something like:
```
Generating word search puzzle...
Horizontal words: ["THIR", "SIX", "THREE", ...]
Vertical words: ["TWENTY", "ONE", "TWO", ...]

Attempt 1/1000
Found solution with area 361 (19x19)

Successfully generated word search!
Final grid size: 19x19 (area: 361)

Placed words:
  THIR (Horizontal) at (9, 10)
  SIX (Horizontal) at (1, 2)
  ...

Grid:
. . . . . . H . . E . E I G H T F . . 
. . . S I X U . F I V E . . . . O . . 
. . . . . . N . . G . T F . . . U O H
...
```

## Step 5: Development Commands

```bash
# Check code without full build
cargo check

# Run with specific max attempts
cargo run --release -- --input example_words.yaml --max-attempts 500

# Build optimized version
cargo build --release
./target/release/wordsearch_generator --input example_words.yaml

# Run tests (if you add them later)
cargo test
```

## Step 6: Create Your Own Word Lists

Create a new YAML file:
```bash
cat > my_words.yaml << 'EOF'
horizontal:
  - "HELLO"
  - "WORLD"
  - "RUST"

vertical:
  - "CODE"
  - "LINUX"
  - "WSL"
EOF

# Test with your words
cargo run --release -- --input my_words.yaml
```

## Troubleshooting

### If Rust isn't found:
```bash
source ~/.cargo/env
```

### If build fails:
```bash
# Update Rust
rustup update

# Clean and rebuild
cargo clean
cargo build --release
```

### Performance testing:
```bash
# Time the generation
time cargo run --release -- --input example_words.yaml --silent
```

## File Structure

After setup, you should have:
```
wordsearch_generator/
├── Cargo.toml              # Dependencies
├── src/
│   └── main.rs             # Main implementation
├── example_words.yaml      # Test data (numbers)
├── small_example.yaml      # Smaller test case
└── target/                 # Build artifacts (after cargo build)
    └── release/
        └── wordsearch_generator  # Final executable
```

## Next Steps

Once everything is working:

1. **Modify the algorithm**: Edit `src/main.rs`
2. **Add features**: Diagonal placement, different optimization strategies
3. **Create more test cases**: Different word lists in YAML files
4. **Performance tuning**: Adjust `max_attempts`, grid sizing algorithms

## Success Criteria

✅ `cargo build --release` completes without errors  
✅ `cargo run -- --input example_words.yaml` generates a grid  
✅ Grid shows words placed horizontally (right-to-left) and vertically (bottom-to-top)  
✅ Program respects `--silent` flag  
✅ Different word lists work correctly  

The word search generator is now ready for development and use in WSL2!
