# Quiz CLI

Quiz CLI is an interactive command-line quiz game to help learn programming concepts, built with Node.js.

## Features

- Multiple categories of questions (JavaScript, Node.js, General Programming)
- Select how many questions to answer
- Progress bar and results summary
- No external dependencies; uses Node.js built-in modules

## Requirements

- Node.js >= 18.0.0

## Installation

1. Clone the repository:

   git clone https://github.com/JesusDiazContractor/test_app.git
   cd test-app/test-app

2. Install dependencies (no external dependencies are listed; if you use npm init in your environment, run npm install to ensure dev tools are available):

   npm install

## Usage

Run the quiz:

   npm start

This will launch an interactive CLI to choose a category and answer questions.

## Project structure

- index.js - application entrypoint
- src/ - helper modules (input handling, quiz logic, terminal colors)
- data/questions.json - question bank organized by categories

## Contributing

Contributions welcome. Please open an issue or submit a pull request with changes.

## License

This project declares MIT in package.json.
