| Directory | Purpose |
|-----------|---------|
| /         | Root directory - the top-level directory of the filesystem |
| /bin      | Essential user command binaries (e.g., ls, cp, pwd) |
| /boot     | Boot loader files, kernel, and initrd |
| /dev      | Device files (e.g., hard drives, USB devices) |
| /etc      | System-wide configuration files |
| /home     | User home directories (e.g., /home/username) |
| /lib      | Essential shared libraries and kernel modules |
| /media    | Mount point for removable media (e.g., USB drives, CDs) |
| /mnt      | Mount point for temporary filesystems |
| /opt      | Optional application software packages |
| /proc     | Virtual filesystem providing process and kernel information |
| /root     | Home directory for the root user |
| /run      | Run-time variable data |
| /sbin     | System binaries (system administration commands) |
| /srv      | Data for services provided by the system |
| /sys      | Virtual filesystem for system hardware information |
| /tmp      | Temporary files (cleared on reboot) |
| /usr      | Secondary hierarchy for user data (contains most applications) |
| /var      | Variable data (logs, databases, websites, etc.) |

# Linux Commands Reference Guide

## Table of Contents

1. System Information  
2. File and Directory Management  
3. File Permissions  
4. Process Management  
5. System Monitoring  
6. Best Practices  

---

## System Information

### CPU Information
```bash
$ cat /proc/cpuinfo
```
Displays detailed CPU information:

- Processor model and speed  
- Number of cores  
- Cache sizes  
- CPU features  
- Vendor information

**Example output:**
```
processor       : 0
vendor_id       : GenuineIntel
cpu family      : 6
model name      : Intel(R) Core(TM) i7-9750H CPU @ 2.60GHz
cpu cores       : 6
cache size      : 12288 KB
```

### Memory Information
```bash
$ free -m
```
Shows memory usage in mebibytes:

- Total installed RAM  
- Used memory  
- Free memory  
- Shared memory  
- Buffer/cache usage  
- Available memory

**Example output:**
```
              total        used        free      shared  buff/cache   available
Mem:          16384        5432        6234         882        4718        9652
Swap:          4096         128        3968
```

### Storage Information
```bash
$ lsblk
```
Lists all block devices:
```
NAME   MAJ:MIN RM   SIZE RO TYPE MOUNTPOINT
sda      8:0    0   512G  0 disk 
├─sda1   8:1    0   500G  0 part /
└─sda2   8:2    0    12G  0 part [SWAP]
```

### System Version
```bash
$ cat /etc/*release
```
Shows distribution information:
```
DISTRIB_ID=Ubuntu
DISTRIB_RELEASE=22.04
DISTRIB_CODENAME=jammy
```

---

## File and Directory Management

### Basic Navigation Commands

#### Print Working Directory
```bash
$ pwd
```
Shows current directory location:
```
/home/username/documents
```

#### Change Directory
```bash
$ cd                  # Go to home directory
$ cd /path/to/dir     # Go to specific directory
$ cd ..               # Move up one directory
$ cd -                # Go to previous directory
```

### File Listing Commands

#### Basic List
```bash
$ ls                  # List files and directories
$ ls -l               # Long format listing
$ ls -a               # Show hidden files
$ ls -la              # Long format with hidden files
$ ls -lh              # Human-readable sizes
```

**Long format explained:**
```
drwxr-xr-x 2 user group 4096 Jan 2 10:00 Documents
│└┬─┘ └┬┘ │    │     │    │  │    │     │
│ │    │  │    │     │    │  │    │     └── Name
│ │    │  │    │     │    │  └───────────── Time
│ │    │  │    │     │    └─────────────── Date
│ │    │  │    │     └────────────────── Group
│ │    │  │    └─────────────────────── Owner
│ │    │  └──────────────────────────── Number of links
│ │    └─────────────────────────────── Others permissions
│ └────────────────────────────────── Group permissions
└──────────────────────────────────── Owner permissions
```

### File Creation Commands

#### Create Files
```bash
$ touch filename.txt                    # Create empty file
$ touch file1.txt file2.txt             # Create multiple files
$ touch -t 202401021200 file.txt        # Create with specific timestamp
```

#### Create Directories
```bash
$ mkdir dirname                         # Create directory
$ mkdir -p path/to/nested/dir           # Create parent directories
$ mkdir -m 755 secured_dir              # Create with specific permissions
$ mkdir dir1 dir2 dir3                  # Create multiple directories
```

### File Removal Commands

#### Remove Files
```bash
$ rm filename                          # Remove file
$ rm -f filename                       # Force remove without prompt
$ rm file1.txt file2.txt               # Remove multiple files
```

#### Remove Directories
```bash
$ rmdir dirname                        # Remove empty directory
$ rm -r dirname                        # Remove directory and contents
$ rm -rf dirname                       # Force remove directory
$ rm -rv dirname                       # Verbose removal
```

### Copy Commands

#### Copy Files
```bash
$ cp source.txt destination.txt       # Copy file
$ cp file.txt /path/to/directory/     # Copy to directory
$ cp -i file.txt backup.txt           # Interactive copy
$ cp -p file.txt backup.txt           # Preserve attributes
```

#### Copy Directories
```bash
$ cp -r source_dir/ dest_dir/         # Copy directory recursively
$ cp -rv dir1/ dir2/                  # Verbose recursive copy
```

**Common cp options:**
- `-a`: Archive mode (preserve attributes)  
- `-i`: Interactive mode  
- `-r`: Recursive copy  
- `-u`: Update only if source is newer  
- `-v`: Verbose output  
- `-p`: Preserve permissions  

### Move/Rename Commands
```bash
$ mv old.txt new.txt                  # Rename file
$ mv file.txt /path/to/directory/     # Move file
$ mv -i source.txt dest.txt           # Interactive move
$ mv dir1/ dir2/                      # Move/rename directory
```

---

## File Permissions

### View Permissions
```bash
$ ls -l filename
```

**Permission string explained:**
```
-rwxr-xr-x
│└┬┘└┬┘└┬┘
│ │   │  └── Others (read, execute)
│ │   └───── Group (read, execute)
│ └───────── Owner (read, write, execute)
└─────────── File type
```

### Change Permissions
```bash
$ chmod 755 file.txt                  # Change using octal
$ chmod u+x file.txt                  # Add execute for user
$ chmod g-w file.txt                  # Remove write for group
$ chmod o=r file.txt                  # Set read-only for others
```

**Permission numbers:**
- `4`: Read  
- `2`: Write  
- `1`: Execute  

**Common combinations:**
- `755`: rwxr-xr-x (directories)  
- `644`: rw-r--r-- (files)  
- `777`: rwxrwxrwx (full access)

### Change Ownership
```bash
$ chown user:group file.txt           # Change owner and group
$ chown -R user:group directory/      # Recursive ownership change
```

---

## Process Management

### View Processes
```bash
$ ps                                  # Show current shell processes
$ ps aux                              # Show all processes
$ top                                 # Real-time process viewer
$ htop                                # Interactive process viewer
```

### Process Control
```bash
$ kill PID                            # Terminate process
$ kill -9 PID                         # Force terminate
$ killall process_name                # Kill by process name
```

---

## System Monitoring

### System Resources
```bash
$ free -h                             # Memory usage
$ df -h                               # Disk usage
$ du -sh directory/                   # Directory size
$ uptime                              # System uptime
```

### Network
```bash
$ ifconfig                            # Network interfaces
$ netstat -tuln                       # Network connections
$ ping hostname                       # Test connectivity
```

---

## Best Practices

### Safety Tips

- Always use `-i` flag with `rm` for interactive deletion  
- Make backups before major operations  
- Use `-v` flag to see what's happening  
- Double-check before using `rm -rf`  
- Keep regular backups  

### Efficiency Tips

- Use tab completion  
- Use up/down arrows for command history  
- Learn keyboard shortcuts  
- Use wildcards carefully  
- Combine commands with `&&`

### Command Line Shortcuts

- `Ctrl + C`: Cancel current command  
- `Ctrl + Z`: Suspend current process  
- `Ctrl + D`: Exit current shell  
- `Ctrl + L`: Clear screen  
- `Ctrl + A`: Move to beginning of line  
- `Ctrl + E`: Move to end of line  
- `Ctrl + U`: Clear line before cursor  
- `Ctrl + K`: Clear line after cursor
