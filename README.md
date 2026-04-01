# test-app  CLI Quiz

Project Description
-------------------
A small interactive command-line quiz application (ES module) that presents multiple-choice questions by category, tracks progress, and shows results with explanations. Intended for use as a lightweight dev/test quiz or demo CLI. The runnable app lives under test-app/test-app in this repository.

Key Features
------------
- Interactive terminal-based multiple-choice quiz.
- Category selection (e.g., JavaScript, Node.js, General Programming).
- Choose number of questions (All / 3 / 5 where available).
- Progress display and per-question feedback.
- Final results summary with review of incorrect answers and explanations.
- Small, dependency-free codebase using Node.js built-in readline.

Setup Instructions
------------------
Prerequisites
- Node.js >= 18.0.0 (package.json enforces Node 18+ / ES module usage).
- npm (or another Node package manager) for installing dev dependencies if added later.

Installation (from repo root)
1. Change into the app directory:
```bash
cd test-app/test-app
```
2. Install dependencies (none are required now, but run to create lockfile / node_modules):
```bash
npm install
```

Note: There is no package-lock.json checked into the repo currently. Running npm install will create one locally.

How to Run the Project
----------------------
Development / Local run
- Start the CLI from the app directory:
```bash
npm start
```
This runs the entrypoint (index.js) which launches the interactive quiz.

Direct node run
```bash
node index.js
```
(from the test-app/test-app directory)

Tests
- package.json contains a test script (`node --test`) but there are no tests in the repository at the time of writing.
```bash
npm test
```
Running this currently does not execute tests because none are present.

Configuration
-------------
- Questions data: test-app/test-app/data/questions.json
  - Each question object is expected to have:
    - `question` (string)
    - `options` (array of strings)
    - `answer` (index of correct option)
    - optional `explanation` (string)
- No .env or runtime configuration files are used.

Project Structure
-----------------
(Only key folders/files shown)
- test-app/test-app/
  - index.js  CLI entrypoint (ES module; creates readline interface)
  - package.json  metadata, scripts, Node engine, "type": "module"
  - data/questions.json  question bank (categories + questions)
  - src/
    - input.js  readline helper wrappers (prompt, select, confirm, pressEnter)
    - quiz.js  Quiz class (shuffle, askQuestion, progress/results)
    - colors.js  ANSI color helpers

Usage Example
-------------
Typical session flow:
1. Run `npm start` in test-app/test-app
2. Choose a category from the menu.
3. Choose how many questions to ask.
4. Answer multiple-choice questions by entering the option number.
5. View progress and final summary with incorrect answers and explanations.

Notes, Observations, and Known Limitations
------------------------------------------
- The app uses ES modules (package.json includes "type": "module") and computes __dirname via import.meta.url.
- The questions JSON matches the code expectations (question, options[], answer index).
- The code uses a FisherYates shuffle; original data is not mutated.
- The readline interface is created once and closed on exit, and loading errors are caught in main.

Potential issues / edge cases
- If data/questions.json is missing or malformed, the app will throw and exit (caught and printed). A friendlier error message and dataset validation would improve resilience.
- No validation of question objects: malformed entries (missing options, invalid answer index) could cause runtime errors.
- No tests or CI configuration are present despite a test script in package.json.
- index.js has a shebang and is CLI-ready, but package.json lacks a "bin" entry to make the CLI globally installable.
- shuffle uses Math.random (non-deterministic). For deterministic testing, allow injecting an RNG/seed.
- No signal handling for SIGINT (Ctrl+C)  adding graceful handling to close readline cleanly is recommended.

Suggested Next Steps (prioritized)
----------------------------------
Low-effort, high-value
1. Add a small schema/validation routine for questions.json (verify options is an array, answer is an integer within bounds) and show a friendly error if validation fails.
2. Add graceful SIGINT handling (close readline on Ctrl+C and exit cleanly).
3. Update README to clearly explain commands from repo root vs the app directory (this README implements that).

Medium-effort
4. Add a "bin" entry in package.json to make the app installable as a command-line tool.
5. Add unit tests for core logic (Quiz behavior, shuffle with injected RNG, input helpers).
6. Commit a lockfile (package-lock.json or preferred package manager lock) to improve reproducibility.

Longer-term / optional
7. Add CI (GitHub Actions) to run tests and linters.
8. Add a validate CLI command to check questions files.
9. Add persistence (high scores), more categories, or support for custom question files.

Contributing
------------
- If you want help implementing any of the suggested changes (validation, SIGINT handling, tests), I can prepare changes and a PR. Please confirm which items you want implemented and I will modify the repository accordingly.

License
-------
No LICENSE file detected in the repository. License: Not specified. If you want a license added, common choices are MIT, Apache-2.0, or GPL-3.0  indicate a preference and it can be added.

Contact / Support
-----------------
If anything in this README is inaccurate or you want me to implement the low-effort changes (validation, SIGINT handling, README clarification), tell me which changes to make and I will prepare the edits and a PR patch.


