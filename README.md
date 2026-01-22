# jenkins-parallel-demo

This repository is created to practice **Jenkins pipelines**.

## Features
- Parameterized pipeline
- Parallel stages
- Maven build
- Artifact archiving

## Parameters
- BRANCH: Git branch to build
- ENV: dev / qa / prod

## Pipeline Stages
1. Checkout source code
2. Parallel execution:
   - Maven Build
   - Environment Info
   - Workspace Info
3. Archive artifacts

## Status
Practice completed successfully ✅
