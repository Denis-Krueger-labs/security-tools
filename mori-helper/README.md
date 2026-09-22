# MORI Helper v2

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

A tiny Bash helper for creating clean, repeatable Hack The Box machine workspaces.

Because yes, you *could* manually create the same directories, notes, environment variables, and scan folders every single time.

MORI simply considers that an inefficient use of twelve seconds.

> "You automated twelve seconds of work.
> Lazy? Yes.
> Smart? Also yes."

---

## What MORI Does

Give MORI a machine name and target IP:

```bash
mori-helper Puppy 10.10.11.70
```

and she prepares a workspace under:

```text
~/htb/machines/puppy/
```

including:

```text
puppy/
├── exploits/
├── files/
├── loot/
├── notes.md
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

MORI also:

* stores the target as `TARGET` and `RHOST`
* detects your HTB VPN IPv4 address from `tun0`
* stores that address as `LHOST`
* supports an optional hostname
* generates a Markdown notes template
* generates a basic Nmap scan helper
* creates predictable directories for loot, exploits, screenshots, scripts, and files
* refuses to overwrite an existing machine workspace
* judges you when appropriate

---

## Usage

```text
mori-helper <machine-name> <ip> [hostname]
```

### Basic

```bash
mori-helper Puppy 10.10.11.70
```

### With hostname

```bash
mori-helper Puppy 10.10.11.70 puppy.htb
```

MORI will not automatically modify `/etc/hosts`.

Instead, she prints the command for you:

```bash
echo '10.10.11.70 puppy.htb' | sudo tee -a /etc/hosts
```

Because silently editing system configuration would be rude.

---

## Example Output

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

MORI has prepared your target.

Machine : Puppy
Target  : 10.10.11.70
LHOST   : 10.10.15.51
Folder  : /home/user/htb/machines/puppy
Hostname: puppy.htb

"You automated twelve seconds of work.
 Lazy? Yes.
 Smart? Also yes."

Optional /etc/hosts entry:

  echo '10.10.11.70 puppy.htb' | sudo tee -a /etc/hosts

Enter workspace:

  cd '/home/user/htb/machines/puppy'
  source target.env

Initial scan:

  ./scan.sh
```

---

## Installation

Clone or download this repository, then copy the helper into a directory on your `PATH`.

For a user-local installation:

```bash
mkdir -p ~/.local/bin
cp mori-helper ~/.local/bin/mori-helper
chmod +x ~/.local/bin/mori-helper
```

Make sure `~/.local/bin` is included in your `PATH`:

```bash
export PATH="$HOME/.local/bin:$PATH"
```

To make that persistent for Bash:

```bash
echo 'export PATH="$HOME/.local/bin:$PATH"' >> ~/.bashrc
source ~/.bashrc
```

Verify:

```bash
which mori-helper
```

You should get something similar to:

```text
/home/user/.local/bin/mori-helper
```

---

## Generated Environment

Every workspace contains:

```text
target.env
```

Load it with:

```bash
source target.env
```

It defines:

```bash
HTB_NAME
TARGET
RHOST
LHOST
HTB_HOSTNAME
HTB_WORKSPACE
```

For example:

```bash
echo "$HTB_NAME"
echo "$TARGET"
echo "$RHOST"
echo "$LHOST"
```

might produce:

```text
Puppy
10.10.11.70
10.10.11.70
10.10.15.51
```

This is particularly convenient for exploit scripts.

For example:

```python
import os

target = os.environ["TARGET"]
lhost = os.environ["LHOST"]
```

No more repeatedly copying IP addresses between terminals.

---

## Automatic LHOST Detection

If an interface named `tun0` exists, MORI reads its IPv4 address and stores it as:

```bash
LHOST
```

For example:

```text
tun0    10.10.15.51/23
```

becomes:

```bash
export LHOST="10.10.15.51"
```

If `tun0` does not exist, `LHOST` is left empty.

MORI will also point this out:

```text
MORI also noticed that tun0 is missing.

"Perhaps connecting the VPN before requesting
 reverse shells would be strategically sound."
```

---

## Notes Template

Every machine gets a pre-generated:

```text
notes.md
```

with sections for:

* target details
* ports
* services
* web enumeration
* credentials
* interesting files
* users
* findings
* initial access
* privilege escalation
* loot
* user flag
* root flag
* commands and miscellaneous notes

The goal is not to enforce a methodology.

It is simply to prevent this:

```text
notes.txt
notes2.txt
box-notes-final.md
actual-notes.md
thing.txt
```

---

## Initial Scan

Each workspace contains:

```text
scan.sh
```

Run it with:

```bash
./scan.sh
```

The helper runs:

```bash
nmap -Pn -sC -sV
```

against the configured target.

Results are stored using Nmap's `-oA` output format under:

```text
scans/nmap/
```

This produces the standard:

```text
initial.nmap
initial.gnmap
initial.xml
```

files.

MORI does **not** automatically start the scan when creating the workspace.

You decide when traffic is sent to the target.

---

## Existing Workspace Protection

If a workspace already exists, MORI refuses to overwrite it.

Example:

```text
MORI: Absolutely not.

That workspace already exists:

  /home/user/htb/machines/puppy

"I'm a cat, not your data-loss prevention strategy."
```

This is intentional.

MORI Helper should organize work, not destroy it.

---

## Requirements

MORI Helper is intentionally lightweight.

The core helper expects common Linux utilities including:

```text
bash
ip
awk
cut
tr
date
```

The generated scan helper additionally requires:

```text
nmap
sudo
```

For automatic `LHOST` detection, your HTB VPN interface is expected to be named:

```text
tun0
```

---

## Scope

MORI Helper deliberately does **not** try to become a full CTF framework.

It does not:

* connect to the HTB VPN
* spawn HTB machines
* automatically modify `/etc/hosts`
* enumerate targets automatically
* exploit anything
* submit flags
* install pentesting tools
* manage credentials
* replace your notes
* pretend `mkdir` is advanced cybersecurity

It does one small job:

**prepare a predictable machine workspace quickly.**

---

## Why?

My normal HTB setup repeatedly involved the same few steps:

```text
create folder
create scan folder
create notes
remember target IP
find VPN IP
create exploit folder
create loot folder
start enumeration
```

None of those steps are difficult.

That is precisely why they are worth automating.

MORI Helper exists to remove a tiny amount of repetitive friction and let you start working on the actual machine faster.

---

## Naming

MORI is a very judgmental cat.

This is important architectural context.

---

## Safety

Use MORI Helper only with systems you are authorized to test.

The helper itself merely creates local files and, when explicitly requested by the user, the generated `scan.sh` can run Nmap against the configured target.

Always respect the rules and scope of the platform, lab, or environment you are working in.

---

## Version

### MORI Helper v2

Current features:

* HTB workspace generation
* target environment variables
* automatic `tun0` IPv4 detection
* optional hostname handling
* notes generation
* initial Nmap helper
* workspace overwrite protection
* mandatory ASCII cat
* unnecessary but deserved judgment

---

## License

See the repository's `LICENSE` file.

---

```text
              /\_____/\ 
             /  o   o  \
            ( ==  ^  == )
             )         (
            (           )
           ( (  )   (  ) )
          (__(__)___(__)__)

"You find the vulnerability.
 I made the folders.

 We both know who had the harder job."

— MORI
```
