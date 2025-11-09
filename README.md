# artix-live

Building Artix Live ISOs on GitHub Actions.

## Solution to overlayfs issue

The ISO build process uses overlayfs to create the filesystem.
GitHub Actions containers run on an overlayfs filesystem,
and the Linux kernel doesn't support nested overlayfs
(overlayfs on top of overlayfs).

The solution is to use the GitHub Actions workspace directory
(`$GITHUB_WORKSPACE`) for the artools build output. The workspace
is mounted from the host filesystem (ext4), not overlayfs, so it
can be used as an overlayfs upperdir.

## How to build

The workflow runs automatically on push, or can be manually triggered:
1. Go to Actions tab in GitHub
2. Select "Build and Release Artix Live ISO"
3. Click "Run workflow"
4. Approve the workflow if required (for first-time runs)

The ISO will be automatically uploaded to GitHub Releases when the build completes.
