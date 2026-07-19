# macos-ansible

This repo contains an Ansible playbook aimed at automating my setup of macOS
devices. This is Alpha-level quality and not intended for public use for the time
being. More to come on that, maybe.

## What's automated

| Role | Covers |
|---|---|
| `homebrew` | Installs Homebrew, taps, all formulas/casks, and `homebrew-autoupdate` |
| `mac_app_store` | Installs App Store apps via `mas` |
| `macos_settings` | Sets os-level settings |

Package lists and Mac App Store IDs live in [group_vars/all.yml](group_vars/all.yml).

## Prerequisites

1. macOS with Xcode Command Line Tools (`xcode-select --install`).
2. Install Homebrew via the instructions at <https://brew.sh>
3. Install Ansible via Homebrew: `brew install ansible`
4. `ansible-galaxy collection install -r requirements.yml`
5. Sign into your Apple Account (Settings > Apple Account)

## Workflow

### 1. Run the playbook

```shell
ansible-playbook playbook.yml -K
```

The playbook is idempotent, it can be re-run it any time to pick up anything that
was skipped.

### 2. Finish by hand

Unfortunately, not everything can be automated. The following needs done manually:

### Manual Installs

- **VMware Fusion**: <https://archive.org/download/vmwareworkstationarchive/>

#### Per-App Settings

- **1Password**
  - Open at startup
  - Enable SSH agent
  - Enable CLI integration
- **Obsidian**
  - Sync vault to `~/obsidian`

### Non-Automatable Settings.app Settings

- **Wi-FI**
  - Turn off Private Wi-Fi address for home network
- **Bluetooth**
  - Pair devices
- **General**
  - **Date & Time**
    - Enable `Set time zone automatically using current location`
- **Menu Bar**:
  - Enable `Show menu bar background`
  - **Menu Bar Controls**
    - Disable `Spotlight`
    - Enable `Wi-Fi`
    - Disable `Battery`
    - Disable `Focus`
    - Disable `Screen Mirroring`
    - Disable `Display`
    - `Sound` to `Always Show`
    - Disable `Now Playing`
    - Disable `Timer`
- **Touch ID & Password**
  - Enroll a fingerprint.
- **Printers & Scanners**
  - Add printer
