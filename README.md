# React + TypeScript + Vite + Husky Setup

_This project is a minimal React app created with Vite, configured with TypeScript and Husky to enforce type checking and linting before commits._

---

## Getting Started

### 1. Create React Project with Vite

    npm create vite@latest

- Enter your project name.
- Select the React + TypeScript template.
- Navigate into your project folder.
- Install dependencies:

  npm install

### 2. Add TypeScript Type Check Script

Add this script to your `package.json` under `"scripts"`:

    "typecheck": "tsc --build --noEmit"

_This runs TypeScript in build mode and checks for type errors without generating output files._

### Install and Set Up Prettier

    npm install --save-dev prettier

Add a Prettier config file `.prettierrc` with:

    {
      "semi": true,
      "singleQuote": true,
      "trailingComma": "es5",
      "printWidth": 100,
      "tabWidth": 2
    }

Add `.prettierignore` file with:

    node_modules
    dist
    build
    coverage

Add format scripts to `package.json`:

    "scripts": {
      "format": "prettier --check .",
      "format:fix": "prettier --write ."
    }

### 3. Install and Setup Husky

Run the following commands to initialize Husky and install dependencies:

    npx husky-init
    npm install

### 4. Configure Husky Pre-commit Hook

Edit the `.husky/pre-commit` file to include:

    #!/usr/bin/env sh
    . "$(dirname -- "$0")/_/husky.sh"

    echo "🔍 Running Typecheck, Linting, and Prettier (with auto-fix)..."

    npm run typecheck && npm run lint && npm run format:fix && echo "✅ All checks passed!" || {
      echo "❌ Typecheck, Linting, or Prettier failed. Please fix the issues before committing."
      exit 1
    }

**Alternatively, you can use lint-staged for a more targeted approach.**

Run:

    npm install --save-dev lint-staged

Then add the following to your `package.json`:

    "scripts": {
      "precommit": "npm run typecheck && lint-staged"
    },
    "lint-staged": {
      "*.{js,jsx,ts,tsx}": [
        "eslint --fix",
        "prettier --write"
      ],
      "*.{json,md,css,html}": [
        "prettier --write"
      ]
    }

Update your `.husky/pre-commit` file to this:

    #!/usr/bin/env sh
    . "$(dirname -- "$0")/_/husky.sh"

    echo "🔍 Running typecheck and lint-staged..."

    npm run precommit

    if [ $? -eq 0 ]; then
      echo "✅ All checks passed. Proceeding with commit."
    else
      echo "❌ Checks failed. Commit aborted."
      exit 1
    fi

This hook ensures that type checking and linting run before every commit. If either fails, the commit will be blocked.

---

## Usage

Run type checking manually:

    npm run typecheck

Run linting manually:

    npm run lint

_Commit your changes as usual; Husky will automatically run the type check and lint scripts before committing._

---

## Notes

Make sure your `tsconfig.app.json` (or main `tsconfig.json`) includes your source files, usually with:

    "include": ["src"]

You can customize Husky hooks to add other checks or formatters as desired.

---

## Resources

- [Vite Documentation](https://vitejs.dev/)
- [TypeScript Documentation](https://www.typescriptlang.org/docs/)
- [Husky Documentation](https://typicode.github.io/husky/#/)
- [ESLint Documentation](https://eslint.org/docs/latest/)

---

Happy coding! 🚀
