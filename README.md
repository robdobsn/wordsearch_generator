# Word Search Generator

A Rust command-line program for generating word search puzzles with specific constraints:
- Horizontal words read right-to-left
- Vertical words read bottom-to-top
- Optimal grid generation favoring minimal area and square-like shapes

## Requirements

### Windows
- Rust toolchain (from https://rustup.rs/)
- **Either:**
  - Visual Studio Build Tools (recommended)
  - Switch to GNU toolchain: `rustup default stable-x86_64-pc-windows-gnu`
  - Use WSL2/Linux environment

### Why Visual Studio Tools?
This isn't due to our specific dependencies - it's how Rust compilation works on Windows by default. See `MSVC_EXPLANATION.md` for details.

## Installation

1. Install Rust from https://rustup.rs/
2. Install Visual Studio Build Tools with C++ support
3. Clone this repository
4. Build the project:
   ```
   cargo build --release
   ```

## Usage

```
cargo run -- --input example_words.yaml
```

### Command Line Options

- `--input` or `-i`: Path to YAML file containing word lists
- `--silent` or `-s`: Disable progress indication
- `--max-attempts`: Maximum attempts to find optimal solution (default: 1000)

### Input File Format

The input file should be a YAML file with two lists:

```yaml
horizontal:
  - "WORD1"
  - "WORD2"
  # ... more horizontal words

vertical:
  - "WORD3" 
  - "WORD4"
  # ... more vertical words
```

### Example

An example input file `example_words.yaml` is provided with number words.

## Algorithm

The program uses a randomized placement algorithm inspired by the WoSeCon paper, adapted for the specific constraints:

1. Estimates initial grid size based on word lengths and count
2. Randomly places words while respecting direction constraints
3. Optimizes for minimal area and square-like grid dimensions
4. Returns the best solution found within the attempt limit

## Output

The program outputs a text-based grid to the terminal, showing only the used area of the grid. Letters represent placed characters, and dots represent empty spaces.
