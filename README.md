# Quiz CLI (test-app)

## Project Overview

**Quiz CLI** is an interactive command-line quiz game for learning and practicing programming concepts (primarily JavaScript/Node.js).

The app:
- Loads question categories from a local JSON file (`test-app/test-app/data/questions.json`)
- Prompts the user to pick a category and question count
- Runs a scored, multiple-choice quiz session in the terminal

---

## Features

- Interactive terminal UI using Node.js `readline`
- Category selection (e.g., *JavaScript Basics*, *Node.js Fundamentals*, *General Programming*) loaded from JSON
- Configurable quiz length (All / 3 / 5 questions, depending on category size)
- Randomized question order (Fisher–Yates shuffle)
- Immediate feedback after each answer (correct/incorrect + correct option)
- Optional per-question explanations displayed after answering (when present)
- Final score summary with performance message and review of incorrect answers

---

## Architecture Overview

This is a small Node.js CLI application (ES Modules) with a simple separation of concerns:

- **Entry point (`index.js`)**: loads question data, drives the main game loop, and coordinates prompts.
- **Input layer (`src/input.js`)**: wraps `readline` to provide promise-based prompts (`select`, `confirm`, `pressEnter`).
- **Domain/game logic (`src/quiz.js`)**: the `Quiz` class handles shuffling, scoring, progress, and result reporting.
- **Presentation (`src/colors.js`)**: ANSI styling helpers used across the CLI output.
- **Data (`data/questions.json`)**: question bank organized by category.

---

## Technology Stack

### Languages

- JavaScript (Node.js)

### Frameworks

- None

### Libraries

- Node.js built-ins: `readline`, `fs/promises`, `path`, `url`

### Databases

- None (local JSON file used as the question store)

### Infrastructure

- None

### External Integrations

- None

---

## File Structure

```text
repository-root/
└── test-app/
    ├── __MACOSX/                # Metadata artifacts (can be removed)
    └── test-app/
        ├── index.js             # CLI entry point
        ├── package.json         # Node package manifest
        ├── data/
        │   └── questions.json   # Quiz categories + question bank
        └── src/
            ├── colors.js        # ANSI color/styling helpers
            ├── input.js         # readline wrappers (select/confirm/etc.)
            └── quiz.js          # Quiz class (shuffle, scoring, results)
```

### Directory Description

| Path | Description |
|------|-------------|
| `test-app/test-app/index.js` | Program entry point; loads questions and runs the interactive loop |
| `test-app/test-app/src/` | Core modules for input handling, quiz logic, and terminal styling |
| `test-app/test-app/data/questions.json` | Question data organized by categories |
| `test-app/__MACOSX/` | macOS archive metadata committed to repo (non-functional) |

---

## Key Modules and Components

[TO BE PROVIDED]

---

## Prerequisites

[TO BE PROVIDED]

---

## Setup Instructions

[TO BE PROVIDED]

---

## Getting Started

[TO BE PROVIDED]

---

## Usage Examples

[TO BE PROVIDED]

---

## API Overview

[TO BE PROVIDED]

---

## Testing

[TO BE PROVIDED]

---

## Deployment

[TO BE PROVIDED]

---

## Additional Details

[TO BE PROVIDED]

---

## Notes

[TO BE PROVIDED]
