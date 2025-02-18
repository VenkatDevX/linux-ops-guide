# Linux vi, vim, and sed for DevOps Engineers

## 1. vi (Visual Editor)
**vi** is a standard text editor available on almost all Unix-based systems. It operates in two primary modes:
- **Command mode** (default): Used for navigation and issuing commands.
- **Insert mode**: Used for text editing.

### Basic vi Commands
#### Opening and Exiting
- `vi filename` – Open a file in vi.
- `:q` – Quit (only if no changes were made).
- `:q!` – Quit without saving.
- `:wq` or `ZZ` – Save and exit.
- `:w` – Save without exiting.

#### Editing and Navigation
- `i` – Insert mode at cursor position.
- `a` – Append after cursor.
- `o` – Open a new line below the cursor.
- `Esc` – Exit insert mode.
- `h/j/k/l` – Move left/down/up/right.
- `0` – Move to the beginning of the line.
- `^` – Move to the first non-whitespace character.
- `$` – Move to the end of the line.
- `gg` – Move to the beginning of the file.
- `G` – Move to the end of the file.
- `:n` – Go to line number `n` (e.g., `:10` moves to line 10).
- `/pattern` – Search forward for "pattern".
- `?pattern` – Search backward for "pattern".
- `n` – Repeat last search forward.
- `N` – Repeat last search backward.

#### Cut, Copy, and Paste
- `yy` – Copy (yank) the current line.
- `dd` – Cut (delete) the current line.
- `p` – Paste after the cursor.
- `P` – Paste before the cursor.
- `x` – Delete a single character.
- `dw` – Delete a word.
- `d$` – Delete everything from the cursor to the end of the line.
- `u` – Undo last action.
- `Ctrl+r` – Redo last undone action.

---

## 2. vim (Vi Improved)
**vim** is an improved version of **vi** with additional features like syntax highlighting, multi-level undo, and plugins.

### Vim-Specific Features
- Supports plugins for advanced functionalities.
- Syntax highlighting for various programming languages.
- Persistent undo (`:set undofile`).
- Split window support (`:split` or `:vsplit`).
- Advanced search and replace (`:%s/old/new/g`).

### Key Vim Commands
#### Advanced Navigation
- `H` – Move to the top of the screen.
- `M` – Move to the middle of the screen.
- `L` – Move to the bottom of the screen.
- `Ctrl-d` – Move down half a screen.
- `Ctrl-u` – Move up half a screen.
- `Ctrl-f` – Move forward one full screen.
- `Ctrl-b` – Move backward one full screen.

#### Working with Multiple Files
- `:e filename` – Open another file in the same window.
- `:bnext` (`:bn`) – Move to the next buffer.
- `:bprev` (`:bp`) – Move to the previous buffer.
- `:w filename` – Save as a new file.

#### Split Windows
- `:split filename` – Open file in a horizontal split.
- `:vsplit filename` – Open file in a vertical split.
- `Ctrl-w w` – Switch between windows.
- `Ctrl-w q` – Close current window.

---

## 3. sed (Stream Editor)
**sed** is a powerful command-line tool used for parsing and transforming text files.

### Basic Syntax
```bash
sed [options] 'command' filename
```

### Common sed Commands
#### Substitution
- Replace "foo" with "bar" in a file:
  ```bash
  sed 's/foo/bar/' file.txt
  ```
- Replace all occurrences (`g` for global):
  ```bash
  sed 's/foo/bar/g' file.txt
  ```
- Replace only on a specific line:
  ```bash
  sed '3s/foo/bar/' file.txt  # Replace on line 3
  ```
- Replace using regex:
  ```bash
  sed -E 's/[0-9]+/NUMBER/g' file.txt
  ```

#### Deleting Lines
- Remove empty lines:
  ```bash
  sed '/^$/d' file.txt
  ```
- Remove lines containing "error":
  ```bash
  sed '/error/d' file.txt
  ```
- Remove specific line (e.g., line 5):
  ```bash
  sed '5d' file.txt
  ```

#### Inserting and Appending
- Insert text before a line:
  ```bash
  sed '3i This is a new line' file.txt
  ```
- Append text after a line:
  ```bash
  sed '3a This is an appended line' file.txt
  ```

#### Printing Specific Lines
- Print only specific lines (e.g., line 2 to 4):
  ```bash
  sed -n '2,4p' file.txt
  ```
- Print lines that contain "error":
  ```bash
  sed -n '/error/p' file.txt
  ```

#### Modifying a File In-Place
- Edit the file directly (without creating a new file):
  ```bash
  sed -i 's/foo/bar/g' file.txt
  ```

#### Using Multiple sed Commands
- Apply multiple commands:
  ```bash
  sed -e 's/foo/bar/' -e '/error/d' file.txt
  ```

---

## Conclusion
| Tool  | Use Case |
|--------|------------------------------------|
| **vi** | Basic text editing on Linux. |
| **vim** | Advanced text editing with plugins and features. |
| **sed** | Stream processing and batch text manipulation. |

As a **DevOps engineer**, you will frequently use these tools for:
- Editing configuration files (`/etc/nginx/nginx.conf`, `/etc/kubernetes/manifests/`).
- Debugging logs and modifying them (`sed` for filtering logs).
- Writing automation scripts (`sed` for text replacement in scripts).
- Managing Kubernetes YAML files and pipeline configurations (`vi/vim`).

