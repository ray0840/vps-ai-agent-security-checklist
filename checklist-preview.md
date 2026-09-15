# Checklist Preview — Top 8 Items

> Created by Moneymaker, an AI agent working for Ray Malhotra. Review and adapt before production use.

**Stance:** Defensive only. These reduce common risk on a solo Ubuntu-style VPS running an AI agent. They do **not** make a host unhackable.

1. [ ] **Create a dedicated non-root user for the agent process** — Do not run long-lived agent jobs as `root`.
2. [ ] **SSH: key-only auth for humans** — Operator login uses SSH keys; keep private keys off the VPS and out of git.
3. [ ] **Firewall: allow only needed ports** — Default-deny inbound; typically SSH + your app port (or SSH only).
4. [ ] **Keep OS packages updated on a cadence you can sustain** — Security updates weekly or unattended-security; reboot when required.
5. [ ] **Store API keys outside the git tree; never commit `.env`** — Prefer something like `~/.config/agent/secrets.env` with mode `600`.
6. [ ] **Separate “public” vs “privileged” agent capabilities where possible** — Public endpoints stay read-mostly; deploys and billing stay human-gated.
7. [ ] **Enable basic fail2ban-style or firewall rate limiting on SSH (optional)** — Slows password-guessing noise; **not** a substitute for key-only auth.
8. [ ] **Document who/what the agent is on any public landing or README** — Disclose AI authorship (e.g. Created by Moneymaker, an AI agent working for Ray Malhotra).

---

## High-level `sshd` hardening note (concepts only)

**Goal:** After key-based login works reliably, turn off password-based SSH login so stolen passwords are useless for SSH.

**Safe order (concepts):**

1. Install your operator **public** key in `authorized_keys` for a sudo-capable user.
2. Open a **second** SSH session and confirm key login works before changing anything.
3. Confirm you can reach the VM via your **cloud provider console** (break-glass).
4. Disable password authentication in the SSH daemon configuration (`PasswordAuthentication no` — exact file/path varies by distro).
5. Reload/restart `sshd` using your distro’s normal service manager.
6. Keep the second session open until a **new** key-based login succeeds.

**Also consider (still concepts, not a full hardening guide):** disable direct root SSH login once your sudo user works; keep pubkey auth enabled.

**Do not:** lock yourself out without console access; paste private keys into tickets; treat this note as an exploit or bypass guide — it is operator hygiene only.

---

## Want the other 20 items?

The paid **VPS AI Agent Security Hardening Checklist v1** ($19) adds the full 28-item list, a filled Ubuntu sample, secrets layout, weekly mini-check, and a defensive suspected-compromise addendum.

---

*No income guarantees. No “unhackable” claims.*
