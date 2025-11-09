# Solutions for Overlayfs in Docker

## Problem
The ISO build fails because:
- GitHub Actions container uses overlayfs as the root filesystem
- buildiso tries to create a nested overlayfs (overlay on top of overlay)
- Linux kernel doesn't allow overlayfs as upperdir of another overlayfs

## Solution Options

### Option 1: Run without container (RECOMMENDED)
Instead of running in a Docker container, run directly on the ubuntu-latest runner and install Artix tools via a different method.

### Option 2: Use tmpfs for working directories
Mount buildiso workspace on tmpfs which is supported as overlayfs upperdir.

### Option 3: Use different container options
Try using volume mounts or different storage drivers.

### Option 4: Patch artools to use fuse-overlayfs
Use fuse-overlayfs instead of kernel overlayfs (complex).
