# Contributing to shinanigans-Dapp

## Continuous Integration (CI) Pipelines

All pull requests targeting `main` must pass automated CI checks before merging.

1. **Contracts CI (`.github/workflows/CI.yaml`)**:
   - Pins Rust 1.96.0 toolchain and wasm32-unknown-unknown target.
   - Executes `cargo fmt`, `cargo clippy`, `cargo test`, and `cargo build --workspace`.
   - Compiles all contracts to release WASM and verifies size budgets.

2. **Backend CI (`.github/workflows/backend-ci.yml`)**:
   - Provisions `postgres:16` and `redis:7` service containers.
   - Executes `npm run lint`, `npm run test:cov`, and `npm run build` in `web/backend`.
   - Validates that code coverage meets specified thresholds.

3. **Frontend CI (`.github/workflows/frontend-ci.yml`)**:
   - Executes `npm run lint`, `npm run type-check`, and `npm run build` in `web/frontend`.

### Branch Protection Configuration

To enforce CI compliance on `main`:

1. Navigate to **Repository Settings** > **Branches**.
2. Add or edit the protection rule for `main`.
3. Enable **Require status checks to pass before merging**.
4. Search for and select the following status check job names:
   - `Backend Lint, Test & Build`
   - `Frontend Lint, Type-Check & Build`
5. Enable **Require branches to be up to date before merging**.

### Required Environment Secrets

No repository secrets are required for basic PR validation as test databases run inside GitHub Actions service containers. Deployment pipeline secrets (e.g., `AWS_ACCESS_KEY_ID`, `AWS_SECRET_ACCESS_KEY`) should be added under **Settings** > **Secrets and variables** > **Actions** if extended to continuous deployment.