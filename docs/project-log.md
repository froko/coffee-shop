# Project Log

## Purpose
This documents contains the required shell commands and tweaks to create this mono-repo.

## Steps

### Initial setup
- Create a new project directory
    ```sh
    mkdir coffee-shop
    ```
- Create an empty `package.json` file
    ```sh
    pnpm init
    ```

- Modify the `package.json` file to look like this:
  ```json
  {
    "name": "coffee-shop",
    "version": "1.0.0",
    "description": "Monorepo containing showcase full-stack apps",
    "keywords": ["coffee shop", "showcase", "monorepo"],
    "author": "Patrick Ineichen",
    "license": "MIT",
    "scripts": {
      "test": "echo \"Error: no test specified\" && exit 1"
    }
  }
  ```
  
- Create an empty `pnpm-workspace.yaml` file
  ```sh
  touch pnpm-workspace.yaml
  ```
  
- Modify the `pnpm-workspace.yaml` file to look like this:
  ```yaml
  packages:
    - "apps/*"
    - "libs/*"
  ```

- Create an empty `.gitignore` file
  ```sh
  touch .gitignore
  ```

- Modify the `.gitignore` file to look like this:
  ```gitignore
  # ignore all files starting with . or ~
  .*
  ~*

  # ignore node dependency directories
  node_modules/

  # --------------------------------------------------------
  # BEGIN Explictly Allowed Files (i.e. do NOT ignore these)
  # --------------------------------------------------------

  # track these files, if they exist
  !.editorconfig
  !.git-blame-ignore-revs
  !.gitignore
  !.nvmrc
  ```
  This should be sufficient for the start of the project. We can add more entries along the way.

- Initialize the git repository
  ```sh
  git init
  ```
- Stage all files and create an initial commit
  ```sh
  git add . && git commit -m "chore: Initial commit"
  ```
### Add Nx mono-repo support

- Add `nx` in workspace mode
  ```sh
  pnpm add nx -D -w
  ```

- Create an empty `nx.json` file
  ```sh
  touch nx.json
  ```

- Modify the `nx.json` file to look like this:
  ```json
  {
    "tasksRunnerOptions": {
      "default": {
        "runner": "nx/tasks-runners/default",
        "options": {
          "cacheableOperations": [
            "build",
            "lint"
          ],
          "cacheDirectory": "node_modules/.cache/nx"
        }
      }
    }
  }
  ```
  This will add basic caching support for build and lint tasks.

- Stage and commit all new and modified files
  ```sh
  git add . && git commit -m "chore: Add Nx support"
  ````