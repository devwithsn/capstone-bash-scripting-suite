# Capstone: Bash Scripting Suite for System Maintenance (vS)

A complete, ready-to-submit project implementing the **Bash Scripting Suite** assignment:

- Automated **Backups** with rotation and logging
- **System Updates & Cleanup** across APT/DNF/pacman
- **Log Monitoring** (disk usage, failed SSH logins, top CPU procs) with an optional watch mode
- Integrated **Menu** to run all tasks
- Centralized **config**, **error handling**, and **logging**


## Project Structure
```
.
├── README.md
├── .gitignore
├── config.env.example
├── exclude.example.txt       
└── scripts/
    ├── backup.sh
    ├── log_monitor.sh
    ├── menu.sh
    ├── updates.sh
    └── utils.sh
```

## Quick Start
```bash
cp config.env.example config.env
chmod +x scripts/*.sh
sudo -E bash scripts/menu.sh
```

## Day-wise mapping
- **Day 1**: Implement `backup.sh` (incremental rsync, rotation, logging).  
- **Day 2**: Implement `updates.sh` (package manager detection, update/cleanup).  
- **Day 3**: Implement `log_monitor.sh` (disk usage threshold, failed SSH logins, top CPU; `--follow`).  
- **Day 4**: Integrate via `menu.sh` and shared `utils.sh` (config, logging, helpers).  
- **Day 5**: Test, add error handling/logging improvements and README polish.

## Features
- **Incremental backups** using `--link-dest` (space-efficient). `--dry-run` supported.
- **Retention policy**: delete backup-* folders older than `BACKUP_RETAIN_DAYS`.
- **System updates & cleanup** for Debian/Ubuntu, Fedora/RHEL, and Arch.
- **Log monitor** scans disk usage ≥ threshold, recent failed SSH attempts, and top CPU processes; watch mode refreshes periodically.
- **Unified config** via `config.env`; all scripts write to `suite.log` with timestamps and levels.
- **Menu** for easy operation and demonstration.

## Configuration (`config.env`)
See `config.env.example` for all variables with safe defaults. Key ones:
- `BACKUP_SRC` — space-separated source paths (default: `$HOME`)
- `BACKUP_DEST` — destination directory (default: `/tmp/backups`)
- `BACKUP_EXCLUDES_FILE` — path to exclude patterns file (e.g. `exclude.example.txt`)
- `BACKUP_RETAIN_DAYS` — retention in days (default: 14)
- `DISK_USAGE_WARN` — percent threshold for warnings (default: 85)
- `TOP_CPU_N` — number of CPU-heavy processes to show (default: 5)
- `WATCH_INTERVAL` — seconds between checks in watch mode (default: 10)
- `UPDATES_YES` — attempt non-interactive updates where supported (default: true)
- `SUITE_LOG` — path to suite log (default: `./suite.log`)
