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

### `index.js`

- Loads `data/questions.json` via `fs/promises.readFile`.
- Presents category and question-count selection.
- Creates a `Quiz` instance and iterates until `quiz.isComplete`.
- Shows results and prompts to play again.

### `src/quiz.js` (`Quiz` class)

- Shuffles incoming questions.
- Tracks `currentIndex`, `score`, and an `answers` audit trail.
- `askQuestion(rl)`: prompts the user, checks correctness, prints feedback/explanation.
- `showResults()`: prints summary + a review list of incorrect questions.

### `src/input.js`

- Promise-based wrappers around `readline`.
- `select()` renders a numbered list and validates numeric choice.
- `confirm()` handles y/n prompts.
- `pressEnter()` blocks until Enter.

### `src/colors.js`

- ANSI escape code helpers (`success`, `error`, `warning`, etc.) used to style output.

### `data/questions.json`

- Structure:
  - `categories` object keyed by category id
  - each category has a `name` and `questions[]`
  - each question includes: `question`, `options[]`, `answer` (0-based index), and optional `explanation`

---

## Prerequisites

- **Node.js >= 18** (as specified in `package.json` `engines.node`)
- npm (bundled with Node.js)

---

## Setup Instructions

### Installation

From the repository root:

```bash
cd test-app/test-app
npm install
```

> Note: this project currently has **no external dependencies**, so `npm install` is effectively a no-op, but it keeps standard Node workflows.

### Configuration

No environment variables or external configuration are required.

To add/edit questions, update:

- `test-app/test-app/data/questions.json`

---

## Getting Started

### Running the Application

```bash
cd test-app/test-app
npm start
```

This runs `node index.js`.

### Running Tests

```bash
cd test-app/test-app
npm test
```

> The repository defines the script `node --test`, but no test files were found in the current codebase.

### Building the Application

No build step is required (plain Node.js execution).

---

## Usage Examples

### Start the quiz

```bash
npm start
```

### Typical flow

1. Choose a category (numbered menu)
2. Choose number of questions (All / 3 / 5)
3. Answer each question by entering the option number
4. Review your final score and any incorrect answers
5. Confirm whether to play again (y/n)

---

## API Overview

Not applicable (no HTTP API). This is a local, interactive CLI.

---

## Testing

- Test runner: Node.js built-in test runner (`node --test`) configured in `package.json`.
- Current state: no `test` directory or `*.test.js` files were found, so the test command will likely report **0 tests**.

If you add tests later, common conventions are:
- `test/**/*.test.js` or `tests/**/*.test.js`
- `src/**/*.test.js`

---

## Deployment

No deployment configuration is included. Typical distribution options for a CLI like this are:

- Publish to npm and expose a `bin` entry in `package.json`.
- Package as a standalone binary using tools like `pkg`.

[TO BE PROVIDED] if deployment/publishing is desired.

---

## Additional Details

### Question format

Each question in `data/questions.json` follows this shape:

```json
{
  "question": "...",
  "options": ["...", "..."],
  "answer": 0,
  "explanation": "..." 
}
```

Notes:
- `answer` is a **0-based** index into `options` (e.g., `2` means the 3rd option).
- `explanation` is optional and shown after the user answers.

### Randomization

`src/quiz.js` shuffles the quiz questions for each run using a Fisher–Yates shuffle.

---

## Notes

[TO BE PROVIDED]
