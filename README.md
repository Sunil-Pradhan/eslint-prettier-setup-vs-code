# 🛠️ Setting Up ESLint + Prettier in VS Code

Here's a step-by-step guide to properly set up ESLint and Prettier for a React project using either Next.js or Vite in VS Code.

## 🚀 Step 1: Create Your Project

⚛️ For Next.js:

```javascript
npx create-next-app@latest
```

⚡ For Vite:

```javascript
npm create vite@latest
```

## 📦 Step 2: Install Required Dependencies

Run this command in your project root:


```bash
npm install --save-dev eslint prettier eslint-config-prettier eslint-plugin-prettier eslint-plugin-react eslint-plugin-react-hooks eslint-plugin-jsx-a11y @typescript-eslint/eslint-plugin @typescript-eslint/parser
```
Here's what each installed package does:

- eslint 🔍 – The core linting tool
- prettier ✨ – Code formatter for consistent styling
- eslint-config-prettier ⚡ – Disables ESLint rules that conflict with Prettier
- eslint-plugin-prettier 🤝 – Runs Prettier as an ESLint rule
- eslint-plugin-react ⚛️ – React-specific linting rules
- eslint-plugin-react-hooks 🎣 – Rules for React hooks (like useEffect)
- eslint-plugin-jsx-a11y ♿ – Accessibility rules for JSX
- @typescript-eslint/eslint-plugin 📜 – TypeScript-specific linting rules
- @typescript-eslint/parser 🔮 – Allows ESLint to parse TypeScript code

## ⚙️ Step 3: Initialize ESLint Configuration

Create/Edit an ESLint config file `eslint.config.js` in your project root:


```js
import js from '@eslint/js'
import globals from 'globals'
import reactHooks from 'eslint-plugin-react-hooks'
import reactRefresh from 'eslint-plugin-react-refresh'
import react from 'eslint-plugin-react';
import jsxA11y from 'eslint-plugin-jsx-a11y';
import ts from '@typescript-eslint/eslint-plugin';
import tsParser from '@typescript-eslint/parser';
import prettier from 'eslint-plugin-prettier';

export default [
  // Global ignores
  {
    ignores: ['dist', 'node_modules'],
  },

  // JavaScript / JSX
  {
    files: ['**/*.{js,jsx}'],
    languageOptions: {
      ecmaVersion: 2021,
      sourceType: 'module',
      globals: {
        ...globals.browser,
        ...globals.node,
      },
      parserOptions: {
        ecmaFeatures: {
          jsx: true,
        },
      },
    },
    plugins: {
      react,
      'react-hooks': reactHooks,
      'jsx-a11y': jsxA11y,
      'react-refresh': reactRefresh,
    },
    extends: [
      js.configs.recommended,
      react.configs.recommended,
      reactHooks.configs.recommended,
      jsxA11y.configs.recommended,
      reactRefresh.configs.vite,
    ],
    rules: {
      'no-unused-vars': ['error', { varsIgnorePattern: '^[A-Z_]' }],
      'react/prop-types': 'off',
      'react/react-in-jsx-scope': 'off',
    },
    settings: {
      react: {
        version: 'detect',
      },
    },
  },

  // TypeScript / TSX
  {
    files: ['**/*.{ts,tsx}'],
    languageOptions: {
      parser: tsParser,
      ecmaVersion: 2021,
      sourceType: 'module',
      globals: {
        ...globals.browser,
        ...globals.node,
      },
      parserOptions: {
        ecmaFeatures: {
          jsx: true,
        },
      },
    },
    plugins: {
      '@typescript-eslint': ts,
      react,
      'react-hooks': reactHooks,
      'jsx-a11y': jsxA11y,
      'react-refresh': reactRefresh,
      prettier,
    },
    extends: [
      js.configs.recommended,
      ts.configs.recommended,
      react.configs.recommended,
      reactHooks.configs.recommended,
      jsxA11y.configs.recommended,
      reactRefresh.configs.vite,
    ],
    rules: {
      'no-unused-vars': 'off',
      '@typescript-eslint/no-unused-vars': ['error', { varsIgnorePattern: '^[A-Z_]' }],
      'react/prop-types': 'off',
      'react/react-in-jsx-scope': 'off',
      '@typescript-eslint/explicit-function-return-type': 'off',
      '@typescript-eslint/explicit-module-boundary-types': 'off',
      'prettier/prettier': 'warn',
    },
    settings: {
      react: {
        version: 'detect',
      },
    },
  },
];
```

## 💅 Step 4: Create Prettier Configuration

Create a `.prettierrc` file in your project root:


```js
{
  "semi": true,
  "trailingComma": "es5",
  "singleQuote": true,
  "printWidth": 100,
  "tabWidth": 2,
  "useTabs": false,
  "jsxSingleQuote": false,
  "bracketSpacing": true,
  "arrowParens": "always",
  "endOfLine": "auto"
}
```
Optionally, create a `.prettierignore` file:

```bash
node_modules
.next
dist
build
```

## 🔌 Step 5: Configure VS Code

1. Install these VS Code extensions:

- ESLint
- Prettier - Code formatter

2. Add these settings to your VS Code `settings.json` (File > Preferences > Settings > Open Settings JSON):


```js
{
  // ========== Personal Preferences (Non-Shareable) ========== //


  // ========== Project Formatting (Shareable) ========== //
  // Prettier Defaults
  "editor.defaultFormatter": "esbenp.prettier-vscode",
  "editor.formatOnSave": true,
  "prettier.requireConfig": true,
  "prettier.singleQuote": true,
  "files.trimTrailingWhitespace": true,
  "files.insertFinalNewline": true,


   // ESLint Integration
  "editor.codeActionsOnSave": {
    "source.fixAll.eslint": "explicit"
  },
  "eslint.validate": ["javascript", "javascriptreact", "typescript", "typescriptreact"],

  // ========== Language-Specific Formatters ========== //
  // JS/TS (Prettier)
  "[javascript]": {
    "editor.defaultFormatter": "esbenp.prettier-vscode"
  },
  "[javascriptreact]": {
    "editor.defaultFormatter": "esbenp.prettier-vscode"
  },
  "[typescript]": {
    "editor.defaultFormatter": "esbenp.prettier-vscode"
  },
  "[typescriptreact]": {
    "editor.defaultFormatter": "esbenp.prettier-vscode"
  },


   // HTML/CSS (VS Code Defaults)
  "[html]": {
    "editor.defaultFormatter": "vscode.html-language-features"
  },
  "[css]": {
    "editor.defaultFormatter": "vscode.css-language-features"
  },
  "[scss]": {
    "editor.defaultFormatter": "vscode.css-language-features"
  },


  // Other Languages


 // Emmet
  "emmet.excludeLanguages": ["markdown"],
  "emmet.extensionsPath": [""],
  "emmet.includeLanguages": {
    "javascript": "javascriptreact"
  }

}
```

## 📜 Step 6: Add Scripts to package.json

Add these scripts to your `package.json`:


```js
"scripts": {
  "lint": "eslint . --ext .js,.jsx,.ts,.tsx",  // 🚨 Find errors
  "lint:fix": "eslint . --ext .js,.jsx,.ts,.tsx --fix", // 🔧 Auto-fix
  "format": "prettier --write \"src/**/*.{js,jsx,ts,tsx,css,scss,json}\"" // ✨ Format
}
```
**🔧 How to Use These Scripts**

1. `npm run lint` 🚨

- Checks all `.js`, `.jsx`, `.ts`, `.tsx` files for errors
- Shows warnings and errors without fixing them
- Useful for CI/CD pipelines to ensure code quality

2. `npm run lint:fix` 🔧

- Same as lint but automatically fixes fixable issues
- Corrects simple problems (e.g., missing semicolons, quotes)
- Some issues may still require manual fixes

3. `npm run format` ✨

- Formats all files in src/ matching: `.js`, `.jsx`, `.ts`, `.tsx`, `.css`, `.scss`, `.json`
- Overwrites files with formatted versions (non-destructive)

**💡 Note**

- Run `npm run lint` **before commits** to check for issues
- Use `npm run lint:fix` first to **automatically fix** what's possible
- Run `npm run format` if you want to **format all files at once**


## 🧪 Step 7: Test Your Setup

1. Create a messy test file 🗑️
2. Save it → should auto-clean 🧹
3. Run commands manually:

```js
npm run lint      # 🚨 Check
npm run lint:fix  # 🔧 Fix
npm run format    # ✨ Beautify
```
