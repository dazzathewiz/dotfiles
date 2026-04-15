# Dotfiles

This repository contains my personal shell and CLI configuration, designed to be deployed automatically via Ansible as part of my Mac bootstrap process.

## Overview

These dotfiles define:

- Shell behaviour (`zsh`)
- Git configuration
- Terminal prompt (via `starship`)
- Environment variables required for my workflows

The goal is to provide a **reproducible, minimal, and portable** setup for new machines.

---

## Contents

| File | Purpose |
|------|--------|
| `.zshrc` | Main shell configuration (aliases, prompt init, environment setup) |
| `.profile` | Environment variables (e.g. SOPS configuration) |
| `.gitconfig` | Git identity and defaults |
| `.config/starship.toml` | Prompt configuration for `starship` |
| `.osx` | OSX defaults configuration |

---

## Requirements

These dotfiles assume the following tools are installed:

- [`zsh`](https://www.zsh.org/)
- [`starship`](https://starship.rs/)
- [`git`](https://git-scm.com/)

In my setup, these are installed automatically via Ansible.

---

## Usage

These dotfiles are not intended to be manually copied. They are deployed via Ansible using the `geerlingguy.dotfiles` role.

Example configuration:

```yaml
dotfiles_repo: https://github.com/dazzathewiz/dotfiles.git
dotfiles_repo_local_destination: ~/Development/GitHub/dotfiles

dotfiles_files:
  - .zshrc
  - .profile
  - .gitconfig
  - .config/starship.toml
  - .osx
```

## ⚠️ Not Managed by `.osx`

The following macOS settings are **intentionally not automated**. These are either:

- user preference / low-value to codify
- brittle across macOS versions
- controlled by third-party apps
- or not reliably configurable via `defaults`

### 🍎 Menu Bar (Status Bar)

Menu bar configuration is **not enforced**.

This includes:
- Visibility of system icons (Wi-Fi, Bluetooth, Battery, etc.)
- Ordering/position of icons
- Control Center modules (Focus, Now Playing, etc.)
- Third-party menu bar apps (e.g. VPN clients, utilities)

**Reason:**
- Apple does not provide stable automation interfaces
- Settings frequently change between macOS versions
- Third-party apps manage their own menu bar presence

**Recommended approach:**
- Configure manually via System Settings → Control Center
- Treat as personal preference

---

### 🖥️ Desktop / Mission Control Layout

Not enforced:
- Number of desktops (Spaces)
- Assignment of apps to specific desktops
- Desktop wallpaper per Space

**Reason:**
- Highly personal workflow preference
- Dynamic by nature
- Not reliably scriptable

---

### ⌨️ Keyboard & Input Edge Cases

Not explicitly configured unless added manually:
- Key repeat rates
- Input sources / languages
- Modifier key remapping

**Reason:**
- Defaults are acceptable
- Preferences vary between users/devices

---

### 📸 Screenshot Location

Screenshot location is not set.

**Default behaviour:**
- Saves to Desktop

**Reason:**
- Low impact
- Easy to change if desired

---

## Design Principles

- **Minimal** – Only include what is required for a productive shell  
- **Portable** – Avoid machine-specific paths where possible  
- **Secure** – No secrets or private keys are stored in this repo  
- **Reproducible** – Works cleanly on a fresh machine  

---

## Security

This repository intentionally excludes:

- SSH keys (`~/.ssh`)
- SOPS keys (`~/.sops`)
- Kubernetes configs (`~/.kube`)
- Any tokens, credentials, or secrets

Sensitive data is managed separately via secure automation.

---

## Notes

- `starship` is used for prompt rendering and must be installed for the prompt to work correctly  
- The environment variable `SOPS_AGE_KEY_FILE` assumes keys are provisioned separately  

---

## Future Improvements

- Split configs into base vs environment-specific layers  
- Add VSCode settings and extensions management  
- Expand shell aliases and tooling  

---

