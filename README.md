# DevOps Multi-Cloud Journey: Linux Fundamentals

This repository documents my daily progress learning Linux for multi-cloud infrastructure and DevOps automation based on course materials by Mr. Ram.

---

## 📅 Day 1: Linux Introduction
* Introduction to open-source operating systems.
* Understanding why Linux forms the backbone of multi-cloud environments.
* Differentiating user roles: Normal Users vs. Superusers (Root).

## 📅 Day 2: Linux Architecture
* Studied the operational layers of Linux:
  * **Hardware:** Physical execution components.
  * **Kernel:** Core engine managing hardware allocation.
  * **Shell:** Command-line interpreter (e.g., Bash) bridging user input to the kernel.
  * **User Space:** Area where user applications and commands execute.

## 📅 Day 3: Filesystem Hierarchy Standard (FHS)
* Explored the universal Linux directory blueprint:
  * `/` (Root directory - parent of all files).
  * `/etc` - Crucial system configuration files.
  * `/bin` & `/sbin` - Vital system binary command execution folders.
  * `/home` - User-specific data storage locations.
  * `/root` - Dedicated home space for the system administrator.

## 📅 Day 4: Hypervisors & CentOS/RHEL Installation
* Theoretical breakdown of virtualization layers and Type-2 hosted hypervisors.
* Set up **VMware** on a Windows host desktop environment.
* Provisioned an independent virtual environment and successfully installed **CentOS 10 / RHEL 10**.

## 📅 Day 5: Linux Basic Commands
### 👤 Login Procedure & Command Prompts
* **Normal User:** Login: `rani` | Password: `password` -> Prompt shows symbol: `$`
* **Super User:** Login: `root` | Password: `password` -> Prompt shows symbol: `#`

### ⚙️ Command Syntax & Structure
* Standard structure: `$command -[options] [arguments]`
* Commands are typically 2 to 5 characters long and strictly **case-sensitive**.
* **Options** modify execution parameters, are prefixed with a hyphen (`-`), and can be chained together.
* **Arguments** designate what target files or directories the command acts upon.
* *Emergency Escape:* Use `Ctrl + D` instead of powering down if critical terminal input errors occur.

### ℹ️ Getting Help Commands
* `man <command>` - Full system manual layout. (Press `q` to quit).
* `man -f <keyword>` - Provides a quick, single-line summary description of a command.
* `info <command>` - Detailed, node-navigated, user-friendly informational guides.
* `<command> --help` - Rapid, built-in functional overview summary text.

### 🖥️ Basic Environment Commands
* `pwd` - Print Present Working Directory location path.
* `date` - Outputs or sets the system date/time metrics.
* `cal` / `cal [month] [year]` - Renders standard calendar maps.
* `whoami` / `logname` - Identifies the active user identity.
* `uname -a` - Reports complete core kernel and architecture details.
* `df -h` / `free -m` - Analyzes available hard disk storage and system RAM usage.
* `clear` - Wipes clean the current terminal interface history display.

## 📅 Day 6: Managing Files & Directories
* Practical operations for structure control inside the CentOS terminal workspace:
  * `touch <file>` - Generates clean, blank files.
  * `mkdir <folder>` - Deploys a new empty folder directory path.
  * `cp <source> <destination>` - Replicates target files or directories safely.
  * `mv <source> <destination>` - Relocates files or performs text renaming operations.
  * `rm <file>` - Permanently drops isolated files.
  * `rm -rf <folder>` - Recursively and forcefully eradicates directories and contents.
