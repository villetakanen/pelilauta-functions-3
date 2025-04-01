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

