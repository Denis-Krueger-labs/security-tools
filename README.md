# Security Tools

Small security utilities, helpers, experiments, and scripts that were useful enough to earn permanent residency.

Some are practical.

Some automate twelve seconds of work.

Some are supervised by cats.

All of them exist because doing the same annoying thing twice is already one time too many.

---

## Current Residents

### /•᷅‎‎•᷄\੭ MORI Helper

```text
              /\_____/\ 
             /  o   o  \
            ( ==  ^  == )
             )         (
            (           )
           ( (  )   (  ) )
          (__(__)___(__)__)

              M O R I
      target preparation department
```

**Status:** Resident
**Department:** Target Preparation & Documentation Enforcement
**Location:** [`mori-helper/`](./mori-helper/)

MORI is a small Bash helper for preparing consistent Hack The Box machine workspaces.

Give her:

```bash
mori-helper Puppy 10.10.11.70 puppy.htb
```

and she creates a workspace containing:

```text
puppy/
├── exploits/
├── files/
├── loot/
├── notes.md
├── writeup.md
├── README.md
├── scans/
│   ├── nmap/
│   └── web/
├── scan.sh
├── screenshots/
├── scripts/
├── target.env
└── web/
```

She also:

* stores `TARGET` and `RHOST`
* detects the HTB VPN address as `LHOST`
* supports optional hostnames
* generates working notes
* generates a structured technical report
* prepares an initial Nmap helper
* refuses to overwrite existing workspaces
* reminds you to document what you did
* judges you for being lazy
* reluctantly admits that the laziness is efficient

> "You automated twelve seconds of work.
> Lazy? Yes.
> Smart? Also yes."

See the resident's own documentation for installation and usage.

---

## Vacant Rooms

More residents may appear when I once again decide that typing the same command twice constitutes an unacceptable workflow.

Potential tenants include:

```text
enumeration helpers
lab utilities
CTF quality-of-life scripts
reporting helpers
small defensive tools
small offensive tools
things that started with "this is a stupid idea"
```

Admission requirements are simple:

1. It solves an actual problem.
2. I use it more than once.
3. It is small enough that creating an entire dedicated repository would be silly.
4. Preferably it develops an unnecessary amount of personality.

---

## House Rules

Tools in this repository are intended for:

* authorized security testing
* CTFs
* labs
* education
* research
* defensive experimentation

Do not use them against systems you do not own or have explicit permission to test.

Individual tools may have additional scope or usage notes in their own directories.

---

## Building Directory

```text
security-tools/
├── mori-helper/
│   ├── mori-helper
│   ├── README.md
│   └── CHANGELOG.md
└── README.md
```

This will inevitably become less tidy.

MORI has been informed.

---

## Philosophy

This repository is not intended to become another enormous security framework.

There are already excellent tools for scanning, exploitation, reverse engineering, web testing, Active Directory, forensics, and everything else.

These scripts exist in the gaps between them.

The tiny repetitive tasks.

The bits of setup that are too trivial to be difficult but annoying enough to interrupt a workflow.

The things that make me think:

> "I could automate that."

Which is generally how another resident gets evicted from `~/random-scripts/` and moves in here.

---

## Contributions

This is primarily my personal collection of security tooling, but the public residents are here because useful little tools should not necessarily be gatekept.

Bug reports and sensible improvements are welcome.

Attempts to remove MORI's ASCII cat will be reviewed with appropriate suspicion.

---

## Disclaimer

These tools are provided for authorized security research, education, CTFs, and controlled lab environments.

You are responsible for ensuring that your use is permitted by the system owner, platform rules, competition rules, and applicable law.

---

## Property Management

```text
Current residents: at least one
Cats in management: one
Unnecessary automation: encouraged
Documentation: mandatory
```

> "Do not dare forget to write down what you did, mortal."

— MORI
