# React with TypeScript and Vite

This project provides a modern development environment for React applications, utilizing TypeScript as the type system and Vite as the build tool. The configuration includes support for Hot Module Replacement (HMR), optimized ESLint rules, and continuous integration with GitHub Actions.

## Main Features

🚀 Technologies used:

- React 18.x
- TypeScript
- Vite 4.x
- ESLint with advanced configuration
- GitHub Pages for automatic deployment
- GitHub Actions for CI/CD

## Environment Setup

To initialize the project:

```bash
npm create vite@latest . -- --template react-ts
cd .
npm install
```

### ESLint Configuration

The project uses an optimized ESLint configuration to ensure code quality:

```json
{
  "root": true,
  "env": {
    "browser": true,
    "es2021": true
  },
  "extends": [
    "airbnb",
    "airbnb/hooks",
    "airbnb-typescript",
    "plugin:react/jsx-runtime"
  ],
  "parserOptions": {
    "project": ["./tsconfig.json"],
    "ecmaVersion": "latest",
    "sourceType": "module"
  },
  "rules": {
    "@typescript-eslint/quotes": ["error", "double", { "avoidEscape": true }],
    "import/order": [
      "error",
      {
        "groups": [
          "builtin",
          "external",
          "internal",
          "parent",
          "sibling",
          "index"
        ]
      }
    ]
  }
}
```

## Scripts Available

```json
{
  "scripts": {
    "dev": "vite",
    "build": "tsc && vite build",
    "preview": "vite preview",
    "lint": "eslint 'src/**/*.ts{,x}'",
    "lint:fix": "npm run lint -- --fix",
    "test": "vitest",
    "test:ui": "vitest --ui"
  }
}
```

## Continuous Integration with GitHub Actions

The project implements an automated CI/CD pipeline that runs tests and deployment:

```yaml
name: Continuous Integration and Deployment

on:
  push:
    branches:
      - main
  pull_request:
    branches:
      - main

jobs:
  test:
    runs-on: ubuntu-latest
    container: node:20
    steps:
      - uses: actions/checkout@v3
      - run: npm ci
      - run: npm test
      - run: npm run build

  deploy:
    runs-on: ubuntu-latest
    needs: test
    steps:
      - uses: actions/checkout@v3
      - run: npm ci
      - run: npm run build
      - name: Deploy to GitHub Pages
        env:
          GITHUB_TOKEN: ${{ secrets.GITHUB_TOKEN }}
        run: |
          git config --global user.email "roger.faria.outlook.com"
          git config --global user.name "rfaria-dev"
          npx gh-pages -d dist -r https://x-access-token:${GITHUB_TOKEN}@github.com/rfaria-dev/ci-cd-demo-with-github-actions.github.io.git
```

## Project URL

🔗 [https://rfaria-dev.github.io/ci-cd-demo-with-github-actions.github.io/](https://rfaria-dev.github.io/ci-cd-demo-with-github-actions.github.io/)
