# React + TypeScript + Vite + Husky Setup

This project is a minimal React app created with Vite, configured with TypeScript and Husky to enforce type checking and linting before commits.

---

## Getting Started

### 1. Create React Project with Vite

```bash
npm create vite@latest
Enter your project name

Select the React + TypeScript template

Navigate into your project folder

Install dependencies:


npm install
2. Add TypeScript Type Check Script
Add this script to your package.json under "scripts":


"typecheck": "tsc --build --noEmit"
This runs TypeScript in build mode and checks for type errors without generating output files.

3. Install and Setup Husky
Run the following commands to initialize Husky and install dependencies:


npx husky-init
npm install
4. Configure Husky Pre-commit Hook
Edit the .husky/pre-commit file to include:


#!/usr/bin/env sh
. "$(dirname -- "$0")/_/husky.sh"
echo "Running Typecheck and Linting..."
npm run typecheck
npm run lint
echo "✅ All checks passed!"

This hook ensures that type checking and linting run before every commit. If either fails, the commit will be blocked.

Usage
Run type checking manually:


npm run typecheck
Run linting manually:


npm run lint
Commit your changes as usual; Husky will automatically run the type check and lint scripts before committing.

Notes
Make sure your tsconfig.app.json (or main tsconfig) includes your source files, usually with:


"include": ["src"]
You can customize Husky hooks to add other checks or formatters like Prettier or lint-staged if desired.

Resources
Vite Documentation

TypeScript Documentation

Husky Documentation

ESLint Documentation

Happy coding! 🚀
