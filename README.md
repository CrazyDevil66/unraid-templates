# Unraid templates

Community Applications templates by CrazyDevil66.

| App | Template | Support |
| --- | --- | --- |
| n8n | `templates/n8n.xml` | [Issues](https://github.com/CrazyDevil66/unraid-templates/issues) |
| Angebots-tool | `templates/angebots-tool.xml` | [Issues](https://github.com/CrazyDevil66/Angebots-tool/issues) |
| braincut-blur | `templates/braincut-blur.xml` | [Issues](https://github.com/CrazyDevil66/braincut-blur/issues) |

## n8n

A plain template for [n8n](https://n8n.io). It uses the official `n8nio/n8n` image, unchanged, with n8n's own defaults. This template is community maintained and not affiliated with n8n.

### What the template adds

The image runs as UID 1000, while Unraid creates folders for `99:100`, so n8n would fail to start with `EACCES`. Instead of a manual `chown`, the template runs the container as `99:100`:

| Setting | Why |
| --- | --- |
| `--user 99:100` | Runs as Unraid's default user |
| `--tmpfs /home/node/.cache` | n8n needs a writable cache, rebuilt on each start |
| `N8N_USER_FOLDER=/home/node` | Keeps the data at the usual `/home/node/.n8n` |
| `HOME=/home/node/.n8n` | Needed to install community nodes |

### Good to know

- **Time zone:** `GENERIC_TIMEZONE` is n8n's default, `America/New_York`. Set your own, or schedules run at the wrong time.
- **Plain HTTP:** n8n's secure cookie blocks sign-in without HTTPS. Set `N8N_SECURE_COOKIE=false` for LAN access.
- **Your shares:** fill in an Extra Path. The Read/Write Files node may use all three Extra Paths. Do not empty `N8N_RESTRICT_FILE_ACCESS_TO`, that turns n8n's file protection off.
- **Code nodes:** set `NODE_FUNCTION_ALLOW_BUILTIN=fs,path` to use files there.
- **Updates:** `stable` follows n8n's newest stable release, including major versions. Use a fixed tag such as `n8nio/n8n:2.45.7` to stay on one version.
- **Backups:** keep the AppData folder. It holds the database and the encryption key.

## Support

Open an issue in this repository for problems with the template. For n8n itself, see the [n8n community](https://community.n8n.io).
