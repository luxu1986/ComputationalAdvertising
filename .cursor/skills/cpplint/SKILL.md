---
name: cpplint
description: Run cpplint static code analysis on C++ source files. Use when the user wants to lint C++ code, check code style, run static analysis, or before committing C++ changes.
---

# C++ Lint Check (macOS)

Run the same cpplint checks that are executed in the CI build pipeline.

## Prerequisites

Check if cpplint.py exists, install only if needed:

```bash
if [[ ! -f ~/.local/bin/cpplint.py ]]; then
    mkdir -p ~/.local/bin
    curl -fsSL https://raw.githubusercontent.com/cpplint/cpplint/master/cpplint.py \
        -o ~/.local/bin/cpplint.py
    chmod +x ~/.local/bin/cpplint.py
fi
```

## Run Lint (Same as CI Build)

```bash
find ./src -type f \( -name "*.c" -o -name "*.cc" -o -name "*.cpp" -o -name "*.cxx" -o -name "*.h" -o -name "*.hh" -o -name "*.hpp" -o -name "*.hxx" -o -name "*.inc" \) -print0 | xargs -0 python3 ~/.local/bin/cpplint.py --verbose=0 --linelength=120 --counting=detailed --repository=..
```

## Lint Single File

```bash
python3 ~/.local/bin/cpplint.py --verbose=0 --linelength=120 path/to/file.cpp
```

## Common Fixes

### Line too long
Break lines at 120 characters.

### Include order
Reorder: related header → C system → C++ stdlib → other libs → project headers.

### Suppress warnings
```cpp
// NOLINT - suppress all
// NOLINT(category) - suppress specific
```
