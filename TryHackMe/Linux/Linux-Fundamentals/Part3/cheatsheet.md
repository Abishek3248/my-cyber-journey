# Linux Fundamentals - Part 3 Cheatsheet

## File Editing & Downloads
| Command / Concept           | Description                           | Example                  |
|-----------------------------|---------------------------------------|---------------------------------|
| `nano`                      | Simple text editor                     | `nano filename`                  |
| `vim`                       | Advanced text editor                   | `vim filename`                   |
| `wget`                      | Download files from the web            | `wget http://example.com/file`  |
| `scp`                       | Securely copy files to/from remote     | `scp file user@IP:/path`        |
| `python -m http.server`     | Serve files locally via HTTP           | Run in folder to share files     |

## Process Management
| Command / Concept           | Description                           | Example              |
|-----------------------------|---------------------------------------|---------------------------------|
| `ps` / `ps aux`             | View running processes                 | `ps aux | grep process_name`    |
| `top`                       | Monitor system processes dynamically   | `top`                           |
| `kill`                      | Send signals to processes              | `kill -SIGTERM PID`             |
| `&` / `fg`                  | Background / foreground process control| `command &` / `fg %1`           |

## Service Management
| Command / Concept           | Description                           | Example                  |
|-----------------------------|---------------------------------------|---------------------------------|
| `systemctl`                 | Manage services via systemd            | `sudo systemctl start nginx`    |
| `enable` / `disable`        | Auto-start services on boot            | `sudo systemctl enable ssh`     |

## Task Automation
| Command / Concept           | Description                           | Example               |
|-----------------------------|---------------------------------------|---------------------------------|
| `cron` / `crontab`          | Schedule recurring tasks               | `crontab -e`                     |
| Cron format                 | 6 fields: MIN HOUR DOM MON DOW CMD    | `0 5 * * * /path/script.sh`     |
| Wildcards                   | Automate patterns                      | `*` (every value)               |

## Package Management
| Command / Concept           | Description                           | Example                  |
|-----------------------------|---------------------------------------|---------------------------------|
| `apt`                       | Install/remove packages                | `sudo apt install package`       |
| Repositories                | Add/remove repos, verify keys          | `sudo add-apt-repository ppa:repo` |

## Log Monitoring & Troubleshooting
| Command / Concept           | Description                           | Example                  |
|-----------------------------|---------------------------------------|---------------------------------|
| `/var/log`                  | System and service logs                | `cat /var/log/syslog`           |
| `tail` / `less`             | View log files easily                  | `tail -f /var/log/syslog`       |

