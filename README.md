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

