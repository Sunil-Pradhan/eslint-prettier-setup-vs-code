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
