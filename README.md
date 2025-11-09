# artix-live

Building Artix Live ISOs on GitHub Actions.

## Solution to overlayfs issue

The ISO build process uses overlayfs to create the filesystem.
GitHub Actions containers run on an overlayfs filesystem,
and the Linux kernel doesn't support nested overlayfs
(overlayfs on top of overlayfs).

The solution is to mount the artools workspace (`/var/lib/artools`)
on tmpfs, which can be used as an overlayfs upperdir.
