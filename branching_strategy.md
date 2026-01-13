# 🌳 Gitflow Branching Strategy

This repository follows the Gitflow workflow to manage development, staging, and production releases.

## 📌 Core Branches

1. `main`

* **Purpose**: Contains the official release history.

* **Status**: Must always be stable and deployable to production.

* **Protection**: Direct commits are forbidden. Changes only arrive via `release/*` or `hotfix/*` branches.

2. `develop`

* **Purpose**: The integration branch for features.

* **Status**: Contains the latest delivered development changes for the next release.

* **Protection**: All features are merged here.

## 🛠 Supporting Branches

### Feature Branches

* **Base Branch:** `develop`

* **Merge Back To:** `develop`

* **Naming Convention:** `feature/JIRA-ID-description` or `feat/short-description`

* **Usage:** Used for developing new features or non-emergency refactors.

### Release Branches

* Base Branch: `develop`

* Merge Back To: `main` and `develop`

* Naming Convention: `release/vX.Y.Z`

* Usage: Used for "polishing" a release (bug fixes, documentation, and version bumping). Once merged into `main`, tag it with the version number.

### Hotfix Branches

* **Base Branch:** `main`

* **Merge Back To:** `main` and `develop`

* **Naming Convention:** `hotfix/vX.Y.Z`

* **Usage:** Used for critical production bugs that cannot wait for the next scheduled release.

## 🚀 The Workflow in Practice

### Step 1: Starting a Feature

```bash
git checkout develop
git pull origin develop
git checkout -b feature/JIRA-101-login-form
```

### Step 2: Finishing a Feature (via Pull Request)

* Push your branch to GitHub.

* Open a Pull Request (PR) to merge into `develop`.

* Update the `CHANGELOG.md` under the `[Unreleased]` section.

* Once reviewed and CI passes, merge the PR.

### Step 3: Creating a Release

Once `develop` has enough features for a release:

```bash
git checkout develop
git checkout -b release/v1.1.0
# Perform version bumps and final fixes
```

Merge this branch into **both** `main` and `develop`.

## ✅ Pull Request Requirements
To maintain the integrity of our branches, every PR must:

* Pass all automated CI tests.

* Be approved by at least one peer.

* Include a Changelog entry (checked by Copilot).

* Follow Conventional Commits (e.g., `feat:`, `fix:`, `docs:`, `chore:`).
