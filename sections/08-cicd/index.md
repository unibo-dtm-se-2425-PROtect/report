---
title: CI/CD
has_children: false
nav_order: 9
---

# CI/CD
This section describes the continuous integration and continuous deployment (CI/CD) workflow of the PROtect project. 

### WHAT IS AUTOMATED AND WHY
The project uses GitHub Actions to automate both testing and releases. The entire process of checking code integrity, environment compatibility, and running tests is automated. New SemVer versions (MAJOR.MINOR.PATCH) and the complete CHANGELOG.md are automatically derived from the Git commit history based on Conventional Commits. The final artifact (the Python package distribution) should be automatically built, tagged, and released to PyPI and GitHub Releases (not fully working). </br>
No deployment (CD) can occur unless the code has successfully passed the comprehensive set of compatibility tests (CI). The use of semantic-release ensures that version bumps strictly adhere to Semantic Versioning (SemVer) rules based on commit content, preventing arbitrary or incorrect versioning by developers. 

### HOW THE WORKFLOW IS IMPLEMENTED
- The check.yml workflow is triggered by push and pull_request events.
- Deployment is handled by the deploy job, which calls the reusable deploy.yml workflow.
- The deployment job only runs if the preceding tests pass (needs: test) and the commit is on the master or main branch.
- Unit tests are executed using python -m unittest discover -s tests -t . -p "test_*.py" -v.
- The deploy.yml workflow installs Node.js and runs the core deployment command: npx semantic-release (maybe not fully working).
