# AMP Template - File Browser

Generic Module template for CubeCoders AMP that deploys
[File Browser](https://filebrowser.org) - a single-binary web file manager
with drag-and-drop upload, user management, and public share links.

---

## Files

| File | Purpose |
|---|---|
| `filebrowser.kvp` | AMP GenericModule configuration |
| `filebrowserconfig.json` | AMP UI settings manifest |
| `README.md` | This file |

No shell scripts. No setup scripts. No extra dependencies.

---

## How it works

On **Update**, AMP downloads the File Browser binary from the latest GitHub
release and marks it executable. That is all.

On **Start**, AMP launches `./filebrowser` directly as the managed process.
If no database exists, File Browser bootstraps itself automatically and prints
a randomly generated admin password to the AMP console. Copy it before closing
the console - it is only shown once.

Default credentials if you miss it: username `admin`, password shown in console.
If lost, delete `filebrowser.db` and click Start again.

---

## Setup

1. Add this repo to AMP under **Configuration > Instance Deployment**.
2. Create a new instance and select **File Browser**.
3. Set the **Files Root Directory** to wherever you want files stored.
4. Click **Update** to download the binary.
5. Click **Start**.
6. Note the admin password from the AMP console.
7. Access the UI at `http://your-host:8080`.

---

## Settings

| Setting | Notes |
|---|---|
| Files Root Directory | Where File Browser serves files from. Takes effect on next Start. |
| Site Name | For reference only. Change branding in the File Browser web UI under Settings > Branding. Not applied by AMP. |
| Disable Image Thumbnails | Reduces CPU/memory on low-resource hosts. Takes effect on next Start. |
| Disable Preview Resize | Reduces CPU on image-heavy directories. Takes effect on next Start. |

Port is managed by AMP automatically via `ApplicationPort1`.

---

## User management

All user management (adding users, setting permissions, creating share links)
is done through the File Browser web UI. Log in as admin and navigate to
**Settings > Users**.

---

## Notes

- The binary and database live in `./filebrowser/` within the AMP instance root.
- The files directory defaults to `./filebrowser/files/` and is created
  automatically on first Start.
- File Browser runs as the AMP service user - ensure that user has read/write
  access to the files directory.
- AMP's built-in SFTP is still available for direct admin access alongside
  the File Browser web UI.
