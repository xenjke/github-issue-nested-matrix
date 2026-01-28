# Test Matrix Nesting GitHub Actions

This repository is a minimal test case to reproduce GitHub Actions internal server errors when using 4 levels of nested matrix strategies in reusable workflows.

## Structure

- **test-nested-matrix.yaml** - Entry point (can be triggered manually or on push/PR)
- **level1-markets.yaml** - Matrix on 2 markets
- **level2-clients.yaml** - Matrix on 2 clients
- **level3-services.yaml** - Matrix on 2 services
- **level4-envs.yaml** - Matrix on 2 environments
- **level5-final.yaml** - Final no-op job

## Expected Behavior

With 4 levels of matrix nesting, this should create 2×2×2×2 = 16 final jobs.

## Actual Behavior

GitHub Actions returns internal server errors when attempting to execute workflows with 4 levels of nested matrices.

## How to Run

1. Push to main branch, OR
2. Create a pull request, OR
3. Manually trigger via Actions tab → "Test 4-Level Nested Matrix" → Run workflow

## Root Cause

GitHub Actions has an undocumented limit of **3 nested matrix strategies** in reusable workflows. Exceeding this limit causes internal server errors.
