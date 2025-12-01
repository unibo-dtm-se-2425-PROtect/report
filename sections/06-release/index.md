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
_Ex. the first times the problem for the already existing file was that the code was not able to correctly generat the new `.tar.gz` and `.whl`, so I triggered them manually and I could go from version 0.1.0 to version 1.1.1. The subsequent times, this procedure stopped working. Other solutions that I tried were pushing the release manually with `npm semantic release` and other errors occurred, some were solved but not all. The release task is still problematic_

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

We chose a MIT License because it’s the most adequate choice for academic projects that are just for didactic purposes and not intended to be used in organizations, it is permissive, clear and easy to use, it’s often utilized in the Python world and it’s ideal if we want the others to freely check and see our code, protecting responsibility anyways. 

## Choice of the versioning schema

The chosen versioning scheme is Semantic Versioning (SemVer), typically represented as **MAJOR.MINOR.PATCH** (MAJOR for breaking changes, MINOR for new features, PATCH for bug fixes). 
The project chose SemVer because it provides a clear, standardized way to communicate the type of changes in a new release to users. This allows consumers to understand the potential impact of upgrading.
The version numbers for all produced artifacts (PyPI package and GitHub Release assets) are aligned to ensure consistency for users. 

A new version is created when a commit is pushed to the main or master branch (and passes CI tests). The commit message format determines the version bump:
1) create a new tag `semantic-release` pushes a new git tag (`vX.Y.Z`) to the repository
2) The `@semantic-release/github` plugin automatically creates a new GitHub Release corresponding to the new tag and attaches the build artifacts (`dist/*`)
3) No dedicated release branch is created in this automated flow. Releases are made directly from the main branch (`main` or `master`).



