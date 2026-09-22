# Changelog

All notable changes to MORI Helper will be documented here.

## v2.1.0  Documentation Enforcement Update

### Added

* automatic `writeup.md` generation for every new HTB machine
* structured technical report template containing:

  * executive summary
  * introduction and objectives
  * attack chain
  * tools used
  * reconnaissance
  * service enumeration
  * initial access
  * lateral movement
  * privilege escalation
  * findings summary
  * defensive considerations
  * hardening recommendations
  * lessons learned
* automatic insertion of:

  * machine name
  * target IP
  * hostname
  * creation date
  * Hack The Box platform information
* separate documentation workflow:

  * `notes.md` for chaotic working notes
  * `writeup.md` for the polished technical report
* generated workspace README now documents both note files
* generated workspace tree now includes `writeup.md`
* MORI documentation reminder hidden inside the generated report
* additional terminal reminder after workspace creation

### MORI Says

> "Do not dare forget to write down what you did, mortal.
> Future-you will not remember that weird curl command."

### Changed

* workspace documentation now separates active investigation notes from publication-ready reporting
* MORI has expanded from Target Preparation Department into Documentation Enforcement
* successful workspace creation now explicitly shows the generated technical report path

### Philosophy

Commands without context become archaeology.

MORI refuses to participate in archaeology.

---

## v2.0.0  MORI Arrives

### Added

* MORI branding
* mandatory judgmental cat
* Hack The Box workspace generation
* automatic `tun0` IPv4 detection for `LHOST`
* `TARGET`, `RHOST`, `LHOST`, `HTB_NAME`, `HTB_HOSTNAME`, and `HTB_WORKSPACE` environment variables
* optional hostname support
* generated `notes.md`
* generated per-machine `README.md`
* initial Nmap scan helper
* organized directories for:

  * scans
  * web enumeration
  * exploits
  * loot
  * files
  * scripts
  * screenshots
* protection against accidentally overwriting an existing workspace
* warning when the HTB VPN interface cannot be detected
* optional `/etc/hosts` command generation
* appropriate criticism of inefficient manual directory creation

### Changed

* transformed a boring workspace bootstrap script into something with considerably more cat

### MORI Says

> "You automated twelve seconds of work.
> Lazy? Yes.
> Smart? Also yes."

---

## Known Issues

* MORI cannot find the vulnerability for you
* MORI refuses responsibility for `final_final_REAL.py`
* MORI cannot force you to actually update `writeup.md`
* MORI can, however, judge you for not doing so
* user may become dependent on having a cat prepare all future infrastructure
