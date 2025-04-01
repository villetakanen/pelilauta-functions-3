# Project init

*Planned, and done initialization memo*

## Phase 1: Foundation & Setup (Node 20, Single Package Focus)

Target Node.js Version Confirmed:
* Action: We will explicitly target Node.js 20, as it's the current stable LTS version well-supported by Firebase Cloud Functions (as of early 2025).
* Rationale: Provides stability, long-term support, and compatibility with Firebase Functions.

## Repository Setup on GitHub:

* Action: Create a new Git repository on GitHub.
* Action: Clone the repository locally.
* Action: Create a .gitignore file in the root of the repository. Include standard Node ignores (node_modules/), Firebase specifics (.firebase/, firebase-debug.log, *.log), editor files, OS files, and importantly, the build output directory that will live inside functions (e.g., functions/lib/). Also add .env.
```env
# Node
node_modules/
npm-debug.log*
yarn-debug.log*
yarn-error.log*
pnpm-debug.log*
lerna-debug.log*
.pnpm-store/

# Firebase
.firebase/
firebase-debug.log*
*.log

# Build output (inside functions dir)
functions/lib/

# Env
.env
.env.*

```
* Rationale: Establishes version control on GitHub and ignores unnecessary files, including the compiled JavaScript output from TypeScript.

##  Node.js Version Management:

*Action: Create a .nvmrc file in the root of the repository containing exactly:
```
20
```
* Action (Recommended): Ensure team members use a Node Version Manager (nvm, fnm) and run nvm use or fnm use upon entering the project directory root.
* * `nvm install && nvm use` (or `fnm install && fnm use`) will automatically set the Node.js version to 20.
* Rationale: Enforces Node.js 20 across development environments.

## Firebase Project Initialization (Creates the functions directory):

* Action: From the root of your cloned repository, ensure firebase-tools is available (pnpm add -g firebase-tools or corepack enable && pnpm dlx firebase-tools).
* Action: Log in: firebase login.
* Action: Initialize Firebase Functions: firebase init functions.
* * Select "Use an existing project" and choose your Firebase project.
* * Select "TypeScript".
* * When asked "Do you want to use ESLint...", select No.
* * When asked "Do you want to install dependencies with npm now?", select No.
* Action: This creates the crucial functions/ directory containing tsconfig.json, package.json, and src/index.ts. This functions directory is now the heart of your project.
* Rationale: Configures the project structure for Firebase Functions with TypeScript, skipping default tooling we'll replace.

## Package Management Setup (Inside functions directory):

* Action: Navigate into the newly created functions directory: cd functions.
* Action: Modify the functions/package.json file created by Firebase:
Ensure "main": "lib/index.js" (or matches your tsconfig.json outDir).

Add the Node.js engine requirement:
```JSON

"engines": {
  "node": "20"
},
```

Review other fields like name, description.

* Action: Run `pnpm install` inside the functions directory. This reads functions/package.json and installs initial dependencies (firebase-admin, firebase-functions) using pnpm, creating functions/pnpm-lock.yaml and functions/node_modules/.
Rationale: Establishes pnpm as the package manager specifically for the functions package and installs its core dependencies. All subsequent package operations (pnpm add, pnpm update) should be run from within this functions directory.

## TypeScript Configuration (Inside functions directory):

* Action: Review and potentially customize functions/tsconfig.json. Key settings:
```
target: "ES2022" (compatible with Node 20).
module: "CommonJS".
outDir: "./lib" (ensure this matches package.json main and .gitignore).
rootDir: "./src".
sourceMap: true.
strict: true.
```
* Rationale: Fine-tunes the TypeScript compiler settings within the functions package. Paths are relative to functions/tsconfig.json.