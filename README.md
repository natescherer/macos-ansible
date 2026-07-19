# macos-ansible

Ansible playbook that automates as much of `buildguide.md` as macOS
reasonably allows. It runs *against the Mac itself* (`ansible_connection=local`)
— there's no separate control node.

## What's automated

| Role | Covers |
|---|---|
| `homebrew` | Installs Homebrew, taps, all formulas/casks, and `homebrew-autoupdate` |
| `mac_app_store` | Installs App Store apps via `mas` (requires you already be signed in) |
| `macos_defaults` | Dark mode, Dock behavior, default browser (via `duti`), `.ics` → Outlook, Touch ID for sudo |
| `chezmoi` | `chezmoi init` |
| `manual_checklist` | Creates `~/obsidian`, then prints everything left to do by hand |

Package lists and Mac App Store IDs live in [group_vars/all.yml](group_vars/all.yml).

## What's not automated, and why

A chunk of `buildguide.md` is inherently manual on modern macOS:

- **Sign-ins / pairing / enrollment**: Apple Account, Bluetooth pairing, Touch
  ID enrollment, printer setup, Bitwarden login — these need a human and/or
  biometric hardware.
- **Control Center, menu bar, and window-tiling toggles**: Apple has moved
  most of these into protected, version-specific plists (or TCC-gated UI
  state) with no stable `defaults write` key, and they change across macOS
  releases. Scripting them would be a coin flip on whether it silently does
  nothing. They're listed as a checklist instead.
- **In-app settings**: Bitwarden's SSH agent/startup/biometrics toggles and
  MEGAsync's backup configuration are app-internal GUI settings.
- **VMware Fusion**: manual download, gated behind a Broadcom account.

The `manual_checklist` role prints all of this at the end of the run so
nothing gets forgotten.

## Prerequisites

1. macOS with Xcode Command Line Tools (`xcode-select --install`).
2. Install Homebrew via instructions at https://brew.sh
3. Install Ansible via Homebrew: `brew install ansible`
2. Ansible on the Mac itself: `python3 -m pip install --user ansible` (or
   `pipx install ansible`).
3. `ansible-galaxy collection install -r requirements.yml`

## Running

```shell
ansible-playbook playbook.yml -K
```

`-K` prompts for your sudo password, needed for the Touch ID for sudo task.

The playbook is idempotent — re-run it any time, e.g. after signing into the
App Store or Apple Account, to pick up anything that was skipped.

## Running a subset

```shell
ansible-playbook playbook.yml -K --tags homebrew
```

Each role is tagged with its own name (`homebrew`, `mac_app_store`,
`macos_defaults`, `chezmoi`, `manual_checklist`).
