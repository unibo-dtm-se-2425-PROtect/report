---
title: Release
has_children: false
nav_order: 7
---

# Release

The release process for this project is automated using semantic-release and targets two main repositories. 
The PROtect project produces two primary artifacts:
1) Source Distribution (`.tar.gz`): The source code archive.
2) Built Distribution (`.whl`): The universal wheel, a package format for faster installation that includes compiled files.
These artifacts are generated in the dist/ directory during the release process.

The artifacts are released to the following repositories:
- **PyPI** (Python Package Index): This is the official third-party software repository for Python, used to distribute the package (`PROtect-UniBo`) so users can install it easily using tools like pip.
- **GitHub Releases**: The built artifacts (`dist/*`) are attached to a new release tag created directly on the GitHub repository. This provides a durable, versioned download link for each release.

The release is automated via a GitHub Actions workflow using **semantic-release**.
The process is triggered automatically when a push occurs on the master or main branch, only after the continuous integration (CI) tests have passed.
_**ATT!** Right now on PyPi only versions until 1.1.1 have been released, even though the `CHANGELOG.dm` file has (correctly) registered more fixes and new feats that made the semantic versioning increase. The problem seems to be a bad request from from https://upload.pypi.org/legacy/ (the 0.1.0 file already exists, which is correct, but it does not seem able of recognizing the fact that new release files should be produced after various version updates). In the present moment, no solution has been found despite many diverse attempts, this is the reason why the version released on PyPi does not match the current actual version of the project_

The automated process is configured in the `.github/workflows/deploy.yml` and `release.config.js` files:
Dependencies Setup The workflow installs Python and `Node.js` dependencies, including the core semantic-release tool:
`pip install -r requirements-dev.txt`
`npm install`

Release Trigger The following command executes the semantic release process, which determines the next version, generates release notes, builds the artifacts, and publishes them:
`npx semantic-release`

The release.config.js file customizes the publishing step to first build the Python package distributions using the standard Python build toolchain:
`python -m build`

The resulting artifacts are then uploaded to the configured repositories:
`python -m twine upload dist/* (to PyPI)`
The `@semantic-release/github` plugin handles creating the GitHub release and uploading `dist/*` as assets.

## Choice of the license

- Which license did you choose for your artefacts? Why?
- Which license did you choose for your code? Why?

## Choice of the versioning schema

- Which versioning schema (e.g. date-based versioning, SemVer, etc.) did you choose for your artefacts? Why?
   + how does the versioning schema work?

- In case of multiple artefacts, are the version numbers aligned or each artefact has its own versioning pace? Why?

- Describe when and how to create a new version of the artefacts in your project
   + e.g. when to increment the major, minor, and patch version numbers
   + e.g. how to create a new release branch
   + e.g. how to create a new tag
   + e.g. how to create a new release on GitHub

