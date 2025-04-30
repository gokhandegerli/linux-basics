### Basic Linux Training from Scratch

#### GNU/Linux Fundamentals

GNU/Linux is an operating system family built upon the Linux kernel, which is free and open-source, combined with the tools and philosophy of the GNU Project. It has a layered structure:

*   **User Space:** The layer where applications, desktop environments, and users directly interact.
*   **Kernel:** The central component that manages communication between hardware and software, controlling system resources (CPU, memory, I/O devices).
*   **Hardware:** The physical components of the computer (CPU, RAM, disk, network card, etc.).

#### Linux Distributions (Distro)

These are fully-fledged operating systems based on the Linux kernel, with various software added on top (desktop environment, package manager, applications). There are hundreds of different distributions, each potentially catering to different purposes and user groups. One of the main differences between distributions is the package management system they use:

*   **apt (Advanced Package Tool):** The package manager used in Debian-based distributions like Debian and Ubuntu. It manages packages with the `.deb` extension.
*   **yum (Yellowdog Updater, Modified) / dnf (Dandified YUM):** Package managers used in Red Hat-based distributions like Red Hat, CentOS, Fedora. They manage packages with the `.rpm` extension. (DNF is the modern successor to YUM.)
*   **WSL (Windows Subsystem for Linux):** Not a Linux distribution itself, but a compatibility layer that allows running Linux command-line tools, utilities, and applications directly on the Windows operating system.

#### User Interfaces and Access

The primary ways to interact with Linux systems:

*   **GUI (Graphical User Interface):** Offers visual interaction through windows, icons, and menus (e.g., GNOME, KDE, XFCE).
*   **CLI (Command Line Interface):** Interaction with the system via text-based commands.
*   **Terminal Emulator:** Applications that provide access to the CLI within a GUI environment (e.g., GNOME Terminal, Konsole, xterm).
*   **Shell:** The interface program that interprets commands received from the user and passes them to the kernel (e.g., Bash, Zsh, Fish).
*   **TTY (Teletypewriter):** Refers to the historical "teletypewriter" devices where a physical keyboard and printer were connected. These are virtual consoles that allow direct text-based input/output to the system, even without a GUI. Typically accessed via `Ctrl + Alt + F1` through `F6` (or `F7`/`F8`) key combinations.
*   **PTY (Pseudo-TTY):** Fake (pseudo) TTYs used by programs like terminal emulators.

#### Shell Operation and Management

The flow of command processing is generally as follows:
`Shell (CLI)` > `Kernel` > `CPU` > `Hardware`

To change the default shell, the following commands can be used:

*   `chsh -s /path/to/shell_name`: Changes the user's default shell (e.g., `chsh -s /bin/zsh`).
*   Editing the `/etc/passwd` file: The shell path for the relevant user can be manually changed in this file where user information is stored (e.g., `sudo vim /etc/passwd`), but using `chsh` is safer.

To find the location of a tool (shell or another command) on the system:

*   `which command_name`: Shows the full path of the command's executable file (e.g., `which bash`, `which zsh`).

#### Built-in Commands and Aliases

These are commands defined within the shell itself, without a separate executable file.

*   `compgen -b`: Lists all built-in commands.
*   `compgen -a`: Lists all defined aliases (command nicknames).

#### $PATH Environment Variable

A list of directory paths, separated by colons (:), indicating where the shell should search for the executable file of a command when it's run.

*   **System-Wide $PATH Definitions:** Can be defined in files like `/etc/profile`, `/etc/bash.bashrc`, `/etc/environment`.
*   **User-Specific $PATH Definitions:** Defined in files within the user's home directory, such as `~/.bashrc`, `~/.bash_profile`, `~/.profile`, `~/.zshrc` (if using Zsh).

#### Bash Shell Shortcuts (Examples)

*   `Ctrl + L`: Clears the screen (like the `clear` command).
*   `Ctrl + C`: Terminates the currently running command.
*   `Ctrl + D`: Exits the shell (sends EOF - End of File signal).
*   `Ctrl + Z`: Suspends the running command and puts it in the background.
*   `Ctrl + R`: Searches backward through command history.
*   `Ctrl + A`: Moves the cursor to the beginning of the line.
*   `Ctrl + E`: Moves the cursor to the end of the line.
*   `Alt + .` (or `Esc` + `.`): Fetches the last argument of the previous command.
*   `Ctrl + _`: Undoes the last change.

#### Getting Help Methods

*   `help <builtin_command>`: Shows help for the specified built-in command.
*   `command --help` or `command -h`: Shows basic usage information and options for most commands.
*   `man <command>`: Displays the detailed manual page for the command.
    *   `man -k <keyword>` (or `apropos <keyword>`): Searches for manual pages related to the keyword.
*   `info <command>`: Displays `info` pages for some commands, offering more detailed, hyperlinked information.

#### Linux Directory System Hierarchy (FHS - Filesystem Hierarchy Standard)

In Linux, files and directories are organized according to a specific standard structure. Key directories and their purposes:

*   **/ (Root Directory):** The top-level directory of the entire filesystem. All other directories reside under this directory. It's the first filesystem mounted by the kernel during system boot.
*   **/bin (Essential User Binaries):** Contains essential user commands (binaries/executables) like `ls`, `cp`, `mv`, `cat`. Necessary for the system to function even in single-user mode.
*   **/sbin (Essential System Binaries):** Similar to `/bin`, but contains system administration commands typically used only by the system administrator (root), such as `fdisk`, `ifconfig`, `reboot`, `mkfs`.
*   **/dev (Device Files):** Contains special files representing physical (hard disk, keyboard) and virtual devices connected to the system. A reflection of the "everything is a file" philosophy in Linux (e.g., `/dev/sda`, `/dev/tty1`).
*   **/etc (Etcetera - Configuration Files):** Contains system-wide configuration files for programs and services (e.g., `/etc/passwd`, `/etc/fstab`, `/etc/network/interfaces`).
*   **/opt (Optional Add-on Software):** Directory for installing third-party software or non-standard packages. Often, each software installs into its own subdirectory (e.g., `/opt/google/chrome`).
*   **/proc (Process Information):** A virtual filesystem that doesn't take up disk space but provides an interface to information in system memory (kernel, processes, hardware status, etc.) through the filesystem interface (e.g., `/proc/cpuinfo`, `/proc/meminfo`).
*   **/root (Root User Home Directory):** The private home directory for the system administrator "root" user.
*   **/run (Runtime Variable Data):** Contains temporary data generated while the system is running (PID files, sockets). Its content is usually cleared upon system reboot. The modern equivalent of `/var/run`.
*   **/var (Variable Files):** Contains files whose size is expected to grow during system operation (log files `/var/log`, email spools `/var/spool/mail`, web server data `/var/www`, etc.).
*   **/tmp (Temporary Files):** Directory where applications and users create temporary files. Its content is usually deleted upon system reboot.
*   **/usr (Unix System Resources):** Contains the majority of user-installed applications, libraries, and shared data. It's like a secondary hierarchy (`/usr/bin`, `/usr/sbin`, `/usr/lib`, `/usr/local`, `/usr/share`). Software not essential for basic system operation is often located here.
    *   `/usr/bin`: User commands (most can be run by normal users).
    *   `/usr/sbin`: System administration commands (usually run by root).
    *   `/usr/lib`: Shared libraries used by applications.
    *   `/usr/share`: Architecture-independent data (documentation, icons, fonts, etc.).
    *   `/usr/local`: Hierarchy reserved for software installed locally (outside the package manager), e.g., `/usr/local/bin`, `/usr/local/lib`.
*   **/home (Home Directories):** Contains personal home directories for normal users (e.g., `/home/john`, `/home/jane`). Users' personal files, documents, and settings are stored here.
*   **/boot (Boot Loader Files):** Contains files necessary for booting the operating system (Linux kernel `vmlinuz`, `initramfs`, bootloader `GRUB` configuration, etc.).
*   **/lib (Essential Shared Libraries):** Contains shared library files (`.so`) and kernel modules required by the essential commands in `/bin` and `/sbin`.
*   **/mnt (Mount Point):** A generally empty directory used by the system administrator as a temporary mount point for filesystems (other disk partitions, network shares).
*   **/media (Removable Media Devices):** Directory where removable media devices like USB drives, CD/DVD drives are typically automatically mounted.
*   **/srv (Service Data):** Directory for site-specific data served by the system (e.g., web server files `/srv/www`, FTP data `/srv/ftp`).

#### Basic Filesystem Commands

##### pwd (Print Working Directory)

*   Prints the full path of the current working directory to the screen.

##### cd (Change Directory)

*   Allows navigation between directories.
*   **Relative Path:** Describes the target directory relative to the current directory (e.g., `cd Documents`, `cd ../Music`).
*   **Absolute Path:** Describes the target directory starting from the root directory (`/`) (e.g., `cd /home/gokhan/Documents`, `cd /etc/nginx`).
*   `cd -`: Returns to the previous working directory.
*   `cd` (without arguments): Navigates to the user's home directory (`/home/username`).
*   `cd ..`: Moves up one directory level.
*   **Quotes and Escape Character:**
    *   `''` (Single Quotes): Treats all characters within them literally (including `$`, `*`), ignoring their special meanings. Provides bulk escaping.
    *   `""` (Double Quotes): Treats most characters literally but preserves the special meaning of some characters like `$`, `\`, ``` ` ``` (backtick) (allows variable expansion, command substitution, escape character).
    *   `\` (Backslash - Escape Character): Removes the special meaning of the immediately following special character (space, `*`, `$`, `(` etc.), treating it as a normal character. Example: `cd new\ folder` navigates to the directory named "new folder" (containing a space).

##### ls (List Directory Contents)

*   Lists the contents of a directory.
*   `ls -l`: Provides a detailed listing in long format (permissions, owner, group, size, date, filename).
    *   `-rw-r--r-- 1 gokhan staff 1590684 Mar 25 21:19 Test.png`
        *   `(-)`: File type (`-`: file, `d`: directory, `l`: symbolic link, etc.).
        *   `rw-r--r--`: Permissions (owner `rwx`, group `rwx`, others `rwx`). `r`: read (4), `w`: write (2), `x`: execute (1), `-`: no permission (0). `chmod 755 file` -> gives `rwxr-xr-x` permissions.
        *   `1`: Number of hard links.
        *   `gokhan`: File owner.
        *   `staff`: Group the file belongs to.
        *   `1590684`: File size (in bytes).
        *   `Mar 25 21:19`: Last modification date/time.
        *   `Test.png`: File/directory name.
        *   `@` (on macOS): Indicates the presence of Extended Attributes.
*   `ls -a`: Shows all content, including hidden files (those starting with `.`).
*   `ls -h`: When used with `-l`, displays file sizes in a human-readable format (KB, MB, GB).
*   `ls -s`: Lists files sorted by size (usually largest to smallest) and may show block size.
*   `ls -t`: Sorts files by modification time (newest first).
*   `ls -r`: Reverses the sorting order (e.g., `ls -trl` -> lists from oldest to newest).
*   `ls -ld <directory_name>`: Shows the properties of the directory itself (not its contents).
*   `ls -l <file_name>`: Shows the properties of the specified file.
*   `ls -R`: Recursively lists all subdirectories and files.

##### mkdir (Make Directory)

*   Creates new directories.
*   `mkdir dir1 dir2`: Creates multiple directories.
*   `mkdir -p parent_dir/sub_dir/grandchild_dir`: Creates necessary parent directories automatically.

##### rmdir (Remove Directory)

*   Deletes only **empty** directories.

##### rm (Remove)

*   Deletes files or directories.
*   `rm file1 file2`: Deletes the specified files.
*   `rm -r directory_name`: Recursively deletes the directory and all its contents. **Use with caution!**
*   `rm -i`: Prompts for confirmation before deleting (interactive).
*   `rm -f`: Forces deletion without prompting (force). **Use with extreme caution!**

#### Bash Shell Expansion

Before executing a command, the shell evaluates and transforms certain characters or expressions on the command line. This process is called shell expansion. The order matters: expansion happens first, the final command is determined, and then the command is executed.

*   **`{}` (Brace Expansion):** Generates multiple strings from comma-separated lists or range expressions. Useful for tasks like creating files/directories.
    *   `echo {a,b,c}d` -> `ad bd cd`
    *   `mkdir project{1..5}` -> Creates directories named `project1`, `project2`, `project3`, `project4`, `project5`.
    *   `echo {1..10..2}` -> `1 3 5 7 9` (Start..End..Step)
    *   `echo {a..c}{1..2}` -> `a1 a2 b1 b2 c1 c2`
*   **`~` (Tilde Expansion):**
    *   `~`: Expands to the current user's home directory (`/home/user`).
    *   `~username`: Expands to the specified user's home directory (`/home/username`).
*   **Variable Expansion:** Variable names starting with `$` are replaced with the variable's value.
    *   `echo $HOME` -> Prints the user's home directory.
    *   `echo "User: $USER"` -> Outputs something like `User: gokhan`.
*   **Command Substitution:** Allows using the output of one command within another command.
    *   `$(command)` or ``` `command` ``` (backticks - older method): The command inside is executed, and its output replaces the substitution. `$(...)` is preferred.
    *   `echo "Today's date: $(date)"` -> Outputs something like `Today's date: Wed Apr 30 15:30:00 TRT 2025`.
    *   `files=$(ls *.txt)` -> Assigns the list of `.txt` files in the current directory to the `files` variable.
*   **Arithmetic Expansion:** Used for performing mathematical operations.
    *   `$((expression))` : The mathematical expression inside is calculated, and the result replaces the expansion.
    *   `echo $((5 * 3))` -> Outputs `15`.
    *   `x=10; echo $(($x + 5))` -> Outputs `15`.
*   **Process Substitution:** Treats the output of a command like a temporary file, allowing it to be used as input to another command.
    *   `< (command)` or `> (command)`: The command's output/input is represented by a temporary file path (e.g., `/dev/fd/63`).
    *   `diff <(ls dir1) <(ls dir2)` -> Shows the difference between the contents of `dir1` and `dir2`.
*   **Word Splitting:** After expansions, results not enclosed in quotes are split into words based on the `$IFS` (Internal Field Separator - usually space, tab, newline) characters.
*   **Filename Expansion (Globbing):** Uses wildcard characters (`*`, `?`, `[]`) to find existing file and directory names that match the pattern and adds them as arguments to the command. **Only matches existing file/directory names, does not generate new names.**
    *   `*`: Matches zero or more of any character (doesn't match hidden files starting with `.` unless explicitly specified). `ls *.txt` -> lists all files ending with `.txt`.
    *   `?`: Matches any single character. `ls report?.doc` -> matches files like `report1.doc`, `reportA.doc`.
    *   `[]`: Matches any single character within the brackets. Can specify a range (`[a-z]`, `[0-9]`) or a list (`[abc]`). `ls [abc]*.txt` -> lists `.txt` files starting with `a`, `b`, or `c`.
    *   `[!...]` or `[^...]`: Matches any single character *not* within the brackets. `ls [!0-9]*.log` -> lists `.log` files not starting with a digit.

#### Regex (Regular Expressions)

A special sequence of characters used to search, match, and manipulate specific patterns within text. More powerful and flexible than shell globbing wildcards (`*`, `?`, `[]`). Widely used by tools like `grep`, `sed`, `awk`.

*   **Key Difference:** Globbing (shell expansion) matches filenames, while Regex matches text content. Although some characters look similar, their meanings and scope differ.

#### Working with Textual Data

One of the core principles of the Linux/Unix philosophy is "Everything is a file." Command outputs, keyboard inputs, and even hardware devices are treated as file-like streams (byte streams).

#### Redirection and File Descriptors (fd)

Every running process typically has three standard data streams by default:

*   **`0` - stdin (Standard Input):** The default place the process receives data from (usually the keyboard).
*   **`1` - stdout (Standard Output):** The default place the process sends its normal output to (usually the screen/terminal).
*   **`2` - stderr (Standard Error):** The default place the process sends its error messages to (usually the screen/terminal).

These streams are represented by numbers called file descriptors. Redirection operators allow us to change the destination of these streams:

*   `< file`: Takes standard input from `file` instead of the keyboard. `command < input.txt`
*   `> file`: Redirects standard output to `file` instead of the screen. Overwrites the file if it exists. `ls -l > list.txt`
*   `>> file`: Appends standard output to the end of `file` instead of the screen. Creates the file if it doesn't exist. `echo "New log" >> log.txt`
*   `2> file`: Redirects standard error to `file` instead of the screen. Overwrites the file if it exists. `command_that_might_error 2> errors.txt`
*   `2>> file`: Appends standard error to the end of `file`. `command_that_might_error 2>> errors.txt`
*   `&> file` or `> file 2>&1`: Redirects both standard output and standard error to `file`. The `2>&1` part means "redirect stderr (2) to the current destination (&) of stdout (1)". Order matters (`> file 2>&1`).
*   `|` (Pipe): Connects the standard output (`stdout`) of one command to the standard input (`stdin`) of another command. `ls -l | grep ".txt"`

##### Special Files

*   `/dev/stdin`, `/dev/stdout`, `/dev/stderr`: Symbolic links pointing to fd 0, 1, and 2, respectively. They link to `/proc/self/fd/0`, `/proc/self/fd/1`, `/proc/self/fd/2` based on the running process.
*   `/dev/tty`: Points to the controlling terminal of the process.
*   `/dev/null`: Also known as the "black hole." Any data redirected here is discarded. Used to suppress unwanted output. `command > /dev/null 2>&1` (discards both stdout and stderr).

#### Text Processing Tools

##### cat (Concatenate)

*   Writes the contents of files to standard output (usually the screen) or concatenates files.
*   `cat file.txt`: Displays the content of the file.
*   `cat file1.txt file2.txt`: Displays the contents of two files sequentially.
*   `cat file1.txt file2.txt > combined_file.txt`: Combines the contents of two files and writes them to a new file.
*   `cat -n file.txt`: Displays content with line numbers.

##### tac (cat backwards)

*   Prints the lines of a file in reverse order (last line first).

##### rev (Reverse)

*   Prints the characters on each line of a file in reverse order (line order remains unchanged).

##### touch

*   Creates non-existent files or updates the access/modification timestamps of existing files.
*   `touch new_file.txt`: Creates an empty file named `new_file.txt` (or updates its timestamp if it exists).
*   `touch -a file.txt`: Updates only the access time.
*   `touch -m file.txt`: Updates only the modification time.

##### stat

*   Displays status information about a file or filesystem (inode, size, permissions, timestamps, etc.).
*   `stat file.txt`: Lists detailed information about the file.
    *   `Size`: File size (bytes).
    *   `Blocks`: Number of blocks allocated on disk.
    *   `IO Block`: Block size for I/O operations.
    *   `regular file`/`directory`/`symbolic link`: File type.
    *   `Device`: Device number where the file resides.
    *   `Inode`: The file's unique inode number.
    *   `Links`: Number of hard links pointing to the file.
    *   `Access (Uid/Gid)`: Owner User ID and Group ID.
    *   `Access`, `Modify`, `Change` timestamps.

##### echo

*   Writes the given text arguments or variable values to standard output. Often used in shell scripts to print messages. Does not read from standard input.
*   `echo "Hello World"`
*   `echo "My home directory: $HOME"`
*   `echo -e "First line\nSecond line"`: The `-e` option enables interpretation of backslash escapes like `\n` (newline), `\t` (tab).

##### paste

*   Merges lines from multiple files side-by-side (default delimiter is tab).
*   `paste file1.txt file2.txt`: First line of `file1`, a tab, first line of `file2`; then second lines, and so on.
*   `paste -d ',' file1.txt file2.txt`: Uses a comma as the delimiter.

##### sort

*   Sorts lines of input (from a file or standard input) alphabetically or numerically.
*   `sort file.txt`: Sorts lines alphabetically.
*   `sort -n file.txt`: Sorts lines numerically.
*   `sort -r file.txt`: Sorts in reverse order.
*   `sort -k 2 file.txt`: Sorts based on the second field (column).
*   `ls -l | sort -k 5 -n`: Sorts files numerically by size (5th column).

##### shuf (Shuffle)

*   Randomly shuffles input lines.
*   `shuf file.txt`: Shuffles the lines of the file.
*   `ls | shuf -n 3`: Selects 3 random files/directories from the listing.

##### nl (Number Lines)

*   Prints input lines with line numbers.
*   `nl file.txt`: Numbers non-empty lines.
*   `nl -ba file.txt`: Numbers all lines (including empty ones).

##### wc (Word Count)

*   Counts lines, words, and bytes/characters in a file or standard input.
*   `wc file.txt`: Outputs `line_count word_count byte_count file.txt`.
*   `wc -l file.txt`: Outputs only the line count.
*   `wc -w file.txt`: Outputs only the word count.
*   `wc -c file.txt`: Outputs only the byte count.
*   `wc -m file.txt`: Outputs only the character count (correctly counts multi-byte characters).
*   `ls -1 | wc -l`: Outputs the number of files/directories in the current directory (`ls -1` prints each entry on a new line).

##### Filtering with pipe (|)

It's possible to perform complex operations by connecting the outputs of commands. Each command processes the output of the previous one.

*   `find /etc/ -name "*.conf" -type f 2> /dev/null | sort | nl | head -n 20`: Finds `.conf` files under `/etc` (hiding errors), sorts the results, numbers them, and displays the first 20 lines.
*   This operation could also be done with temporary files:
    `find /etc/ -name "*.conf" -type f 2> /dev/null > found.txt`
    `sort < found.txt > sorted.txt`
    `nl < sorted.txt > numbered.txt`
    `head -n 20 numbered.txt`
    (Using pipes is more efficient and practical.)

##### xargs (Extended Arguments)

*   Reads items (usually line by line) from standard input and builds and executes command lines using those items as arguments. Very useful when needing to pipe into commands that don't accept standard input directly (e.g., `echo`, `rm`, `cp`).
*   `cat files_to_delete.txt | xargs rm`: Passes each line from `files_to_delete.txt` as an argument to the `rm` command.
*   `find . -name "*.tmp" | xargs rm`: Deletes the found `.tmp` files.
*   `find . -name "*.log" -print0 | xargs -0 rm`: Used for filenames that might contain spaces or special characters. `-print0` separates filenames with a null character, and `xargs -0` reads null-separated input. This is a safer method.

##### tee (T Pipe)

*   Reads data from standard input and writes it to both standard output (usually the screen or the next pipe) and one or more specified files. Used to view data in a pipeline while simultaneously saving it.
*   `ls -l | tee file_list.txt | less`: Writes the output of `ls -l` to `file_list.txt` and also sends it to the `less` command.
*   `echo "New setting" | sudo tee -a /etc/configuration.conf`: Appends the text "New setting" from standard output to the end of `/etc/configuration.conf` with `sudo` privileges. The command `sudo echo "..." >> /etc/...` often fails due to permissions because the redirection (`>>`) is handled by the shell before `sudo` grants privileges; `tee` solves this. The `-a` (append) option adds to the end instead of overwriting.

##### grep (Global Regular Expression Print)

*   Searches for a specified pattern (text or regex) in files or standard input and prints the matching lines to standard output.
*   `grep "search_text" file.txt`: Finds lines containing "search_text" in `file.txt`.
*   `cat log.txt | grep "ERROR"`: Pipes the content of `log.txt` to `grep` to filter lines containing "ERROR".
*   `grep -i "text" file.txt`: Performs case-insensitive search (ignore case).
*   `grep -v "text" file.txt`: Shows lines that do *not* contain "text" (invert match).
*   `grep -r "text" /path/to/dir`: Searches for "text" in files within the specified directory and its subdirectories (recursive).
*   `grep -l "text" *.txt`: Lists only the names of `.txt` files containing "text" (list filenames).
*   `grep -n "text" file.txt`: Shows matching lines along with their line numbers.
*   `grep -E "pattern1|pattern2" file.txt`: Uses Extended Regex to find lines containing either "pattern1" or "pattern2". Same function as the `egrep` command.
*   `grep "^start" file.txt`: Finds lines starting with "start".
*   `grep "end$" file.txt`: Finds lines ending with "end".

###### Basic Regex Rules (for grep, sed, awk)

*   `.`: Matches any single character (except newline `\n`).
*   `*`: Matches zero or more occurrences of the preceding character (`a*` -> "", "a", "aa", "aaa"...).
*   `+`: Matches one or more occurrences of the preceding character (`a+` -> "a", "aa", "aaa"...). (Often requires `-E`).
*   `?`: Matches zero or one occurrence of the preceding character (`a?` -> "" or "a"). (Often requires `-E`).
*   `^`: Matches the beginning of the line.
*   `$`: Matches the end of the line.
*   `[]`: Character set. Matches any single character within the brackets (`[abc]`). Ranges can be specified (`[a-z]`, `[0-9]`).
*   `[^...]`: Negated character set. Matches any single character *not* within the brackets (`[^0-9]` -> non-digit).
*   `{n}`: Matches exactly `n` occurrences of the preceding character (`a{3}` -> "aaa"). (Often requires `-E`).
*   `{n,}`: Matches at least `n` occurrences of the preceding character (`a{2,}` -> "aa", "aaa"...). (Often requires `-E`).
*   `{n,m}`: Matches at least `n` and at most `m` occurrences of the preceding character (`a{2,4}` -> "aa", "aaa", "aaaa"). (Often requires `-E`).
*   `|`: Or (Alternation). Matches either of the two patterns (`cat|dog`). (Often requires `-E`).
*   `()`: Grouping. Used to group patterns or capture them (`(ab)+` -> "ab", "abab"...). (Often requires `-E`).
*   `\`: Escapes the special meaning of special characters (e.g., `.`, `*`, `[`, `\`), allowing them to be matched literally. `grep "\." file.txt` -> searches for the literal dot character.

##### find

*   Searches for files and directories within a specified directory tree (including subdirectories) based on various criteria.
*   `find /path/to/dir -name "search_name"`: Finds files/directories with the exact name "search_name" in the specified path. Wildcards (`*`, `?`, `[]`) can be used (usually best enclosed in quotes). `find . -name "*.log"`
*   `find . -iname "search_name"`: Like `-name` but performs a case-insensitive search.
*   `find /path -type f`: Finds only files.
*   `find /path -type d`: Finds only directories.
*   `find /path -type l`: Finds only symbolic links.
*   `find /path -size +10M`: Finds files larger than 10 Megabytes (`+`: greater than, `-`: less than. `k`: Kilobytes, `M`: Megabytes, `G`: Gigabytes).
*   `find /path -mtime +7`: Finds files modified more than 7 days ago (`+`: older, `-`: newer. `mmin` for minutes).
*   `find /path -user username`: Finds files owned by the specified user.
*   `find /path -group groupname`: Finds files belonging to the specified group.
*   `find /path -perm 644`: Finds files with permissions exactly 644. `-perm /644` finds files with at least these permissions.
*   `find /path -empty`: Finds empty files or directories.
*   `find /path -name "*.tmp" -delete`: Finds and deletes `.tmp` files.
*   `find /path -name "*.log" -exec rm {} \;`: Executes the `rm` command for each found `.log` file. `{}` represents the found file, `\;` marks the end of the command. A more efficient alternative: `find /path -name "*.log" -exec rm {} +` (passes multiple files as arguments to a single `rm` command).
*   `find . \( -name "*.txt" -or -name "*.log" \) -type f`: Finds files ending in `.txt` or `.log` (`-or`, `-and` (default), `-not` can be used; parentheses need escaping `\(` and `\)`).
*   `find . -regex ".*\.py$"`: Uses Regex to find files ending in `.py`. `-regex` matches the entire path (not just the filename) against the pattern.

##### locate

*   Uses a pre-built database to quickly find files on the system. Much faster than `find`, but may not find/show newly created/deleted files if the database is outdated.
*   `locate filename`: Searches the database for the filename.
*   `sudo updatedb`: Updates the database used by `locate`. May need to be run after adding/deleting files.

##### cut

*   Extracts specific sections (columns or character ranges) from lines in a file or standard input.
*   `cut -d ':' -f 1 /etc/passwd`: Uses `:` as the delimiter (`-d`) and extracts the 1st field (`-f`) (username) from each line of `/etc/passwd`.
*   `cut -c 1-10 file.txt`: Extracts the first 10 characters (`-c`) from each line.
*   `ls -l | cut -c 50-`: Extracts characters from the 50th position to the end of each line from `ls -l` output (approximates getting filenames).

##### tr (Translate)

*   Translates or deletes characters from data read from standard input.
*   `echo "Hello World" | tr 'a-z' 'A-Z'`: Translates lowercase letters to uppercase -> `HELLO WORLD`.
*   `echo "This:is:a:test" | tr ':' ' '`: Replaces `:` characters with spaces -> `This is a test`.
*   `cat file.txt | tr -d '\r' > new_file.txt`: Deletes Windows carriage return characters (`\r`) (DOS to Unix conversion). `-d` performs deletion.
*   `echo "Repeeeating chaaars" | tr -s 'e'`: Squeezes repeated `e` characters into a single one -> `Repeating chars`. `-s` (squeeze-repeats).
*   `cat /dev/urandom | tr -dc 'a-zA-Z0-9' | fold -w 32 | head -n 1`: Generates a random 32-character alphanumeric password.
    *   `tr -dc 'a-zA-Z0-9'`: Deletes (`-d`) all non-alphanumeric characters (`-c` complement).
    *   `fold -w 32`: Wraps the stream into lines of 32 characters.
    *   `head -n 1`: Takes the first line.

##### sed (Stream Editor)

*   A powerful tool for performing editing operations (find, replace, insert, delete) on text streams (file or standard input). Often used in scripts for automated text processing.
*   Basic Usage: `sed 'command' file.txt` or `command_output | sed 'command'`
*   **`s` (Substitute):** `sed 's/old/new/g' file.txt`
    *   `s`: Substitute command.
    *   `/`: Delimiter character (other characters can be used: `sed 's#old#new#g'`).
    *   `old`: Pattern to search for (text or regex).
    *   `new`: Replacement text.
    *   `g` (global): Replaces all occurrences on the line. If omitted, only the first match is replaced.
    *   Example: `sed 's/apple/orange/g' fruits.txt`
*   **Addressing:** Specifies on which lines the command should be applied.
    *   `sed '3s/a/A/g' file.txt`: Performs substitution only on the 3rd line.
    *   `sed '1,5s/a/A/g' file.txt`: Performs substitution from line 1 to line 5 (inclusive).
    *   `sed '/^#/d' file.txt`: Deletes lines starting with `#` (`d` command). `/.../` uses regex for addressing.
*   **`d` (Delete):** Deletes lines at the specified addresses.
    *   `sed '5d' file.txt`: Deletes the 5th line.
    *   `sed '/^\s*$/d' file.txt`: Deletes empty lines or lines containing only whitespace.
*   **`p` (Print):** Prints lines at the specified addresses. Usually used with the `-n` option (`-n` suppresses default printing).
    *   `sed -n '10p' file.txt`: Prints only the 10th line.
    *   `sed -n '/error/p' log.txt`: Prints lines containing "error" (similar to `grep "error" log.txt`).
*   **`a` (Append):** Appends a new line *after* the line at the specified address.
    *   `sed '3a New appended line' file.txt`: Appends the text after the 3rd line.
*   **`i` (Insert):** Inserts a new line *before* the line at the specified address.
    *   `sed '1i ## Header ##' file.txt`: Inserts the text before the 1st line.
*   **`-e`:** Used to run multiple `sed` commands simultaneously.
    *   `sed -e 's/old1/new1/' -e 's/old2/new2/' file.txt`
*   **`-i`:** Edits the file in-place (modifies the file directly instead of printing to stdout). **Use with caution!** Can be used as `-i.bak` to create a backup.
    *   `sed -i 's/ERROR/WARNING/g' log.txt`

##### awk

*   A powerful text processing and reporting language. It works by splitting lines into records and space-separated sections within lines into fields. Suitable for more complex operations and programming logic than `sed`. `gawk` (GNU awk) is the most common version.
*   **Basic Structure:** `awk 'pattern { action }' file.txt`
    *   `pattern`: Determines which lines to process (regex or condition). If omitted, action applies to all lines.
    *   `action`: Operations to perform on matching lines (often uses `print`). If omitted, the default action is `{ print $0 }` (print the whole line).
*   **Fields:**
    *   `$0`: The entire line (record).
    *   `$1`: The first field.
    *   `$2`: The second field.
    *   `$NF`: The last field (Number of Fields).
*   **Examples:**
    *   `awk '{ print $1 }' file.txt`: Prints the first field of each line.
    *   `awk '{ print $NF }' file.txt`: Prints the last field of each line.
    *   `ls -l | awk '{ print $9 " -> " $1 }'`: Prints the 9th (filename) and 1st (permissions) fields from `ls -l` output.
    *   `awk '/error/ { print $0 }' log.txt`: Prints lines containing "error" (like `grep "error" log.txt`).
    *   `awk '$3 > 100 { print $1, $3 }' data.txt`: Prints the 1st and 3rd fields of lines where the 3rd field is greater than 100.
    *   `awk -F ':' '{ print $1 }' /etc/passwd`: Uses `:` as the field separator (`-F ':'`) and prints the first field (usernames) from `/etc/passwd`.
    *   `awk 'BEGIN { print "Header" } { print $1 } END { print "Total:", NR }' file.txt`: Prints "Header" before processing (`BEGIN`), prints the first field of each line, and prints the total number of records (`NR`) after processing (`END`).

#### Paging Tools (Pagers)

Used to view long outputs page by page on the screen.

##### more

*   Basic paging tool.
*   `ls -l /etc | more`: Displays the output page by page.
*   `Space`: Next page.
*   `Enter`: Next line.
*   `q`: Quit.
*   Does not allow backward scrolling.

##### less

*   A more advanced and flexible pager than `more`.
*   `ls -l /etc | less`: Opens the output with `less`.
*   `Space` or `f`: Next page.
*   `b`: Previous page.
*   `Up/Down Arrow Keys`: Scroll line by line.
*   `/pattern`: Search forward.
*   `?pattern`: Search backward.
*   `n`: Next match.
*   `N`: Previous match.
*   `q`: Quit.

##### head

*   Displays the beginning part (first 10 lines by default) of a file or standard input.
*   `head file.txt`: Shows the first 10 lines.
*   `head -n 5 file.txt`: Shows the first 5 lines.
*   `head -c 20 file.txt`: Shows the first 20 bytes.

##### tail

*   Displays the ending part (last 10 lines by default) of a file or standard input. Very useful for monitoring log files.
*   `tail file.txt`: Shows the last 10 lines.
*   `tail -n 20 file.txt`: Shows the last 20 lines.
*   `tail -c 50 file.txt`: Shows the last 50 bytes.
*   `tail -f log.txt`: Follows the file, displaying new lines as they are added in real-time. Exit with `Ctrl+C`.

#### File and Directory Management

##### cp (Copy)

*   Copies files or directories.
*   `cp source_file target_file`: Copies the file and gives it a new name.
*   `cp source_file target_directory/`: Copies the file into the specified directory.
*   `cp file1 file2 file3 target_directory/`: Copies multiple files into a directory.
*   `cp -r source_directory target_directory/`: Recursively copies the directory and its contents.
*   `cp -i`: Prompts for confirmation before overwriting (interactive).
*   `cp -v`: Shows the files being copied (verbose).
*   `cp -p`: Preserves permissions, ownership, and timestamps during copy (preserve).

##### mv (Move)

*   Moves or renames files or directories.
*   `mv old_name new_name`: Renames the file/directory.
*   `mv source_file target_directory/`: Moves the file into the specified directory.
*   `mv file1 file2 dir1 target_directory/`: Moves multiple files/directories into a directory.
*   `mv -i`: Prompts for confirmation before overwriting.
*   `mv -n`: Does not overwrite existing files (no-clobber).
*   `mv -v`: Shows the files being moved.

##### rm (Remove)

*   Deletes files or directories (details provided earlier). **Use with caution!**

##### shred (Secure Delete)

*   Permanently deletes files by overwriting their content with random data, making recovery difficult. Normal `rm` only removes the file's pointer (inode link); the data itself may remain on the disk until overwritten.
*   `shred file.txt`: Overwrites the file 3 times by default.
*   `shred -n 5 file.txt`: Overwrites 5 times.
*   `shred -u file.txt`: Deletes the file after overwriting (like `rm`).
*   `shred -v file.txt`: Shows the steps of the operation.
*   `shred -z file.txt`: Writes zeros as the final overwrite (to hide the shredding).
*   `shred -uvz -n 10 secret_file.txt`: Overwrites 10 times with random data, then zeros, shows progress, and deletes the file.

#### Links

Pointers that provide access to files or directories using different names.

*   **Hard Link:**
    *   Creates multiple filenames that point to the same file data (the same inode).
    *   Even if the original file is deleted, the file data remains on the disk and accessible as long as a hard link exists.
    *   Can only be created within the same filesystem (partition).
    *   Hard links usually cannot be created for directories (due to the risk of circular references).
    *   Creation: `ln source_file hard_link_name`
    *   The `ls -li` command shows inode numbers and link counts. Hard links share the same inode number, and their link count increases.
*   **Soft Link (Symbolic Link):**
    *   A special file containing the path to another file or directory (like a shortcut in Windows).
    *   Acts as a pointer to the original file or directory.
    *   If the original file is deleted or moved, the soft link becomes broken.
    *   Can be created across different filesystems.
    *   Can be created for directories.
    *   Creation: `ln -s /full/path/to/source_file_or_dir soft_link_name`
    *   The `ls -l` command shows them starting with `l` and indicating the target with `->`.

#### Archiving and Compression

##### tar (Tape Archive)

*   Combines multiple files and directories into a single archive file (`.tar`). By default, it does not compress, only bundles files.
*   **Creating an Archive:** `tar -cf archive_name.tar file1 dir1 ...`
    *   `-c`: Create a new archive.
    *   `-f`: File (Specifies the archive filename. The name must immediately follow this option).
    *   `-v`: Verbose (Lists the files being processed). `tar -cvf archive.tar files/`
*   **Listing Archive Contents:** `tar -tf archive_name.tar`
    *   `-t`: List the contents of the archive.
*   **Extracting Files from Archive:** `tar -xf archive_name.tar`
    *   `-x`: Extract files from the archive.
    *   `tar -xf archive.tar -C /target/directory`: Extracts the archive into the specified target directory.
    *   `tar -xvf archive.tar`: Lists files as they are extracted.
*   **Adding Files to Archive:** `tar -rf archive_name.tar file_to_add`
    *   `-r` or `--append`: Appends files to an existing archive (may not be very efficient).
*   **Deleting Files from Archive:** `tar --delete -f archive_name.tar file_to_delete`
    *   `--delete`: Deletes files from the archive (may not be very efficient).

##### Compression Tools (gzip, bzip2, xz)

*   Used to reduce the size of files. Often used in conjunction with `tar`.
*   **gzip:** A widely used, fast compression tool. Uses the `.gz` extension.
    *   `gzip file.txt`: Compresses `file.txt` into `file.txt.gz` and deletes the original.
    *   `gzip -k file.txt`: Compresses without deleting the original (keep).
    *   `gzip -d file.txt.gz`: Decompresses the file (same as `gunzip file.txt.gz`).
    *   `gzip -r directory/`: Recursively compresses all files in the directory.
*   **bzip2:** Generally offers better compression ratios than `gzip` but is slower. Uses the `.bz2` extension.
    *   `bzip2 file.txt`
    *   `bzip2 -k file.txt`
    *   `bzip2 -d file.txt.bz2` (same as `bunzip2 file.txt.bz2`).
*   **xz:** Usually provides the best compression ratios but is the slowest. Uses the `.xz` extension.
    *   `xz file.txt`
    *   `xz -k file.txt`
    *   `xz -d file.txt.xz` (same as `unxz file.txt.xz`).

##### Archiving and Compressing in One Step (with `tar`)

The `tar` command can invoke compression tools directly.

*   **With gzip:** `tar -czf archive_name.tar.gz directory_or_files`
    *   `-z`: Compress/decompress using gzip.
*   **With bzip2:** `tar -cjf archive_name.tar.bz2 directory_or_files`
    *   `-j`: Compress/decompress using bzip2.
*   **With xz:** `tar -cJf archive_name.tar.xz directory_or_files`
    *   `-J`: Compress/decompress using xz.

*   **Extracting Compressed Archives:**
    *   `tar -xzf archive_name.tar.gz`
    *   `tar -xjf archive_name.tar.bz2`
    *   `tar -xJf archive_name.tar.xz`
    (Often, `tar -xf archive_name` can automatically detect the correct compression method based on the file extension.)

##### Tools for Reading Compressed Files

*   `zcat file.gz`: Prints the contents of a `.gz` file to the screen without decompressing it (same as `gzcat`).
*   `zless file.gz`: Views a `.gz` file with `less` without decompressing it.
*   `zgrep pattern file.gz`: Searches for a pattern within a `.gz` file without decompressing it.
*   `bzcat`, `bzless`, `bzgrep` (for `.bz2`)
*   `xzcat`, `xzless`, `xzgrep` (for `.xz`)

#### System Information Commands

##### date

*   Displays or sets the system date and time.
*   `date`: Shows the current date and time.
*   `date +"%Y-%m-%d %H:%M:%S"`: Shows the date and time in the specified format.

##### cal (Calendar)

*   Displays a calendar.
*   `cal`: Shows the calendar for the current month.
*   `cal 2025`: Shows the calendar for the entire year 2025.
*   `cal 5 2025`: Shows the calendar for May 2025.

##### which

*   Finds the full path of a command's executable by searching the directories listed in the `$PATH` variable.
*   `which ls` -> `/bin/ls` (or similar)
*   `which python`

##### type

*   Indicates the type of a command (alias, keyword, function, builtin, file).
*   `type cd` -> `cd is a shell builtin`
*   `type ls` -> `ls is aliased to 'ls --color=auto'` (if an alias is defined) or `ls is /bin/ls`
*   `type -a command`: Shows all types matching the command name (e.g., if it's both an alias and a file).

##### file

*   Attempts to determine the type of a file by examining its content.
*   `file document.txt` -> `document.txt: ASCII text`
*   `file image.jpg` -> `image.jpg: JPEG image data, ...`
*   `file /bin/bash` -> `/bin/bash: ELF 64-bit LSB executable, ...`

##### lsb_release

*   Shows Linux Standard Base (LSB) and distribution-specific information.
*   `lsb_release -a`: Shows all information (Distributor ID, Description, Release, Codename).

##### uname (Unix Name)

*   Shows basic information about the system kernel and operating system.
*   `uname`: Shows the kernel name (`Linux`).
*   `uname -a`: Shows all information (kernel name, hostname, kernel release, machine architecture, etc.).
*   `uname -r`: Shows the kernel release.
*   `uname -m`: Shows the machine hardware name (architecture) (e.g., `x86_64`).

##### uptime

*   Shows how long the system has been running, the number of current users, and the system load averages.

##### free

*   Shows the amount of total, used, and free memory (RAM) and swap space usage in the system.
*   `free`: Shows amounts in kilobytes by default.
*   `free -h`: Shows amounts in human-readable format (MB, GB).
*   `free -m`: Shows amounts in megabytes.

##### du (Disk Usage)

*   Calculates the disk space occupied by files or directories.
*   `du file.txt`: Shows the space used by the file (usually in kilobyte blocks).
*   `du directory/`: Shows the space used by the directory and each of its subdirectories separately.
*   `du -sh directory/`: Shows the total size of the directory in human-readable format (`-s`: summary, `-h`: human-readable).
*   `du -h --max-depth=1 /home/user`: Shows the sizes of first-level files and directories under the specified path in human-readable format.

##### df (Disk Free)

*   Shows the total size, used space, free space, and mount point for mounted filesystems.
*   `df`: Shows all mounted filesystems (usually in 1K blocks).
*   `df -h`: Shows in human-readable format.
*   `df -T`: Also shows the filesystem type.
*   `df .`: Shows information for the filesystem where the current directory resides.

#### Package Management

Systems that simplify the installation, updating, removal, and management of software (packages) on Linux distributions.

*   **Installation from Source Code:** Before package managers, software was often installed manually by downloading source code, compiling it (`./configure`, `make`, `sudo make install`), and installing it. Dependencies (other libraries and programs required for the software to run) also had to be found and installed manually. While still possible, this method is cumbersome and difficult to manage.
*   **Package Managers:** Automate this process. They download pre-compiled, ready-to-install packages from servers (repositories), automatically resolve and install dependencies, and make updating and removal easy.

##### Debian-Based Systems (Debian, Ubuntu, Mint, etc.)

*   **Package Format:** `.deb`
*   **Low-Level Tool:** `dpkg` (Installs, removes, queries packages directly but doesn't automatically resolve dependencies).
    *   `sudo dpkg -i package_name.deb`: Installs the package.
    *   `sudo dpkg -r package_name`: Removes the package (leaves configuration files).
    *   `sudo dpkg -P package_name`: Removes the package completely (purge).
    *   `dpkg -l | grep package_name`: Checks if the package is installed.
*   **High-Level Tool:** `apt` (Advanced Package Tool - a modern combination of tools like `apt-get`, `apt-cache`). Manages dependencies, finds, downloads, and installs packages from repositories.
    *   `sudo apt update`: Updates package lists from repositories. Recommended before installing/upgrading.
    *   `sudo apt upgrade`: Upgrades installed packages to their latest available versions.
    *   `sudo apt full-upgrade` (or `dist-upgrade`): Works like `upgrade` but will also install/remove packages if necessary to complete the upgrade, potentially changing core system components.
    *   `sudo apt install package_name`: Installs a new package or updates an installed one.
    *   `sudo apt remove package_name`: Removes the package (leaves configuration files).
    *   `sudo apt purge package_name`: Removes the package completely.
    *   `sudo apt autoremove`: Removes packages that were installed as dependencies but are no longer needed.
    *   `apt search keyword`: Searches for packages in repositories based on a keyword.
    *   `apt show package_name`: Shows detailed information about the package.
    *   `sudo apt install -f`: Attempts to fix broken dependencies (fix-broken).
    *   `sudo apt clean`: Clears the cache of downloaded `.deb` packages (`/var/cache/apt/archives/`).
*   **Repository List:** The `/etc/apt/sources.list` file and files in the `/etc/apt/sources.list.d/` directory contain the server addresses (repositories) from which `apt` downloads packages. `sudo apt update` should be run after modifying these files.

##### Red Hat-Based Systems (RHEL, CentOS, Fedora, Oracle Linux, etc.)

*   **Package Format:** `.rpm`
*   **Low-Level Tool:** `rpm` (Manages packages directly, doesn't automatically resolve dependencies).
    *   `sudo rpm -i package_name.rpm`: Installs the package (install).
    *   `sudo rpm -U package_name.rpm`: Updates the package (upgrade), installs if not already present.
    *   `sudo rpm -e package_name`: Removes the package (erase).
    *   `rpm -q package_name`: Queries if the package is installed.
    *   `rpm -qa`: Lists all installed packages.
*   **High-Level Tool:** `yum` (Yellowdog Updater, Modified) or `dnf` (Dandified YUM - the modern, often faster successor to `yum`). Manages dependencies, finds, downloads, and installs packages from repositories. (Commands are generally similar for `yum` and `dnf`; `dnf` is preferred on modern systems).
    *   `sudo dnf check-update` (or `yum check-update`): Lists packages with available updates.
    *   `sudo dnf update` (or `yum update`): Updates all installed packages.
    *   `sudo dnf install package_name` (or `yum install package_name`): Installs a new package.
    *   `sudo dnf remove package_name` (or `yum remove package_name`): Removes a package.
    *   `sudo dnf autoremove` (or `yum autoremove`): Removes dependencies that are no longer needed.
    *   `dnf search keyword` (or `yum search keyword`): Searches for packages in repositories.
    *   `dnf info package_name` (or `yum info package_name`): Shows information about the package.
    *   `sudo dnf clean all` (or `yum clean all`): Clears the package cache.
*   **Repository List:** Files with the `.repo` extension in the `/etc/yum.repos.d/` directory contain repository information.

#### User and Group Management

Linux is a multi-user system. Users and groups are used to manage file access permissions and access to system resources.

##### User Types

*   **Root (Super User):** The special user with User ID (UID) 0, having full privileges over the system. Used for system administration.
*   **System Users:** Users created to run specific services or applications, often without login privileges (e.g., `www-data`, `nobody`). Their UIDs are typically in a specific range (e.g., 1-999).
*   **Normal Users:** Standard users who use the system for daily tasks. Their UIDs are usually 1000 and above. They have limited privileges and cannot modify system files outside their own files.

##### `sudo` Command

Allows normal users to execute commands with `root` privileges (or as another user) temporarily by entering their own password. Which users can run which commands via `sudo` is defined in the `/etc/sudoers` file or files within the `/etc/sudoers.d/` directory. The `sudo visudo` command should be used to edit these files (it performs syntax checking).

##### Creating and Managing Users

*   `sudo adduser new_user`: Interactively creates a new user (includes steps like creating home directory, group, asking for password, etc.). Generally the preferred method.
*   `sudo useradd new_user`: A lower-level command that only creates the user. Options like `-m` (create home directory), `-g` (specify primary group), `-G` (specify supplementary groups), `-s` (specify shell) may need to be added manually.
*   `sudo passwd username`: Sets or changes the password for the user. Necessary to assign a password to a newly created user.
*   `sudo userdel username`: Deletes the user.
*   `sudo userdel -r username`: Deletes the user and their home directory (`/home/username`).
*   `sudo usermod [options] username`: Modifies user properties (e.g., `sudo usermod -aG group_name username` -> adds user to a supplementary group, `sudo usermod -s /bin/zsh username` -> changes their shell).
*   `su - username`: Switches to the specified user (the `-` loads the user's environment variables and home directory). To switch to root, `su -` or `sudo su -` can be used.

##### User Information Files

*   `/etc/passwd`: Contains user account information (username, UID, GID, home directory, shell). Passwords are not stored here. Readable by everyone.
*   `/etc/shadow`: Contains encrypted passwords and password aging information for users. Readable only by `root`.
*   `/etc/group`: Contains group information (group name, GID, members).

##### Group Management

*   When a user is created, a *primary group* with the same name is usually also created, and the user becomes a member. Files created by the user belong to this group by default.
*   Users can also be members of one or more *secondary groups* (supplementary groups).
*   `sudo groupadd new_group`: Creates a new group.
*   `sudo groupdel group_name`: Deletes a group.
*   `sudo groupmod -n new_name old_name`: Renames a group.
*   `sudo gpasswd -a username group_name`: Adds the user to the specified group (as a secondary group).
*   `sudo gpasswd -d username group_name`: Removes the user from the group.
*   `groups`: Lists the groups the current user is a member of.
*   `groups username`: Lists the groups the specified user is a member of.

#### Access Permissions

In Linux, every file and directory has permissions that determine who can do what.

*   **Permission Types:**
    *   `r` (Read): Read file content, list directory contents (`ls`).
    *   `w` (Write): Modify file content, create/delete/rename files/directories within a directory.
    *   `x` (Execute): Run the file as a program, enter the directory with `cd`.
*   **Permission Owners:**
    *   **User (u):** The user who owns the file.
    *   **Group (g):** The group the file belongs to. Permissions apply to users in this group.
    *   **Others (o):** All other users who are not the owner and not in the group.
*   **Representation (in `ls -l` output):**
    *   The first character indicates the file type (`-`: file, `d`: directory, `l`: link).
    *   The next 9 characters represent user, group, and others permissions in 3-character groups: `rwx r-x r--`
        *   `rwx`: Read, write, execute permission.
        *   `r-x`: Read and execute permission, no write permission.
        *   `r--`: Only read permission.
        *   `---`: No permissions.
*   **Numeric (Octal) Representation:** A method to express permissions using a 3-digit number. Each digit represents user, group, others, respectively. Each permission has a numeric value: `r=4`, `w=2`, `x=1`, `-=0`. The values for permissions within a digit are added together.
    *   `rwx` = 4 + 2 + 1 = `7`
    *   `r-x` = 4 + 0 + 1 = `5`
    *   `rw-` = 4 + 2 + 0 = `6`
    *   `r--` = 4 + 0 + 0 = `4`
    *   `---` = 0 + 0 + 0 = `0`
    *   Example: `rwxr-xr--` -> `754`

##### `chmod` (Change Mode)

Used to change the permissions of files or directories. Only the file owner or `root` can use it.

*   **Symbolic Method:** `chmod [ugoa][+-=][rwx] file/directory`
    *   `u`, `g`, `o`, `a` (all): Specifies whose permissions are changing.
    *   `+`, `-`, `=`: Add, remove, or set permissions exactly.
    *   `r`, `w`, `x`: Which permission is affected.
    *   Examples:
        *   `chmod u+x script.sh`: Adds execute permission for the owner.
        *   `chmod g-w report.txt`: Removes write permission for the group.
        *   `chmod o=r document.doc`: Sets permissions for others to read-only.
        *   `chmod a+r secret_dir`: Adds read permission for everyone (listing for directories).
        *   `chmod ug+rw,o-w file.txt`: Adds read/write for user/group, removes write for others.
*   **Numeric (Octal) Method:** `chmod NNN file/directory` (NNN is the 3-digit octal code).
    *   Examples:
        *   `chmod 755 directory`: `rwxr-xr-x` (Owner full access, group/others read/execute). Common for directories.
        *   `chmod 644 file.txt`: `rw-r--r--` (Owner read/write, group/others read-only). Common for regular files.
        *   `chmod 700 secret_script.sh`: `rwx------` (Only owner has full access).
*   **`-R` Option:** Recursively applies the changes to the directory and all its contents.
    *   `chmod -R 755 public_html/`

##### `chown` (Change Owner)

Used to change the owner and/or group of files or directories. Usually only `root` can use it.

*   `sudo chown new_owner file.txt`: Changes the owner of the file.
*   `sudo chown :new_group file.txt`: Changes the group of the file.
*   `sudo chown new_owner:new_group file.txt`: Changes both the owner and the group.
*   `sudo chown -R user:group /path/to/directory`: Recursively changes ownership of the directory and its contents.

##### `chgrp` (Change Group)

Used only to change the group of a file or directory (functions the same as `chown :new_group`).

*   `sudo chgrp new_group file.txt`
*   `sudo chgrp -R new_group /path/to/directory`

#### Disk Management

##### Storage Basics

*   **Bit and Byte:** `1 Byte = 8 Bits`.
*   **Sector:** The smallest physical unit of data that can be read from or written to a disk (typically 512 bytes or 4096 bytes).
*   **Block:** The smallest logical unit of data that the filesystem can address. Usually consists of multiple sectors (e.g., commonly 4096 bytes = 4KB in Linux). A file, no matter how small, occupies at least one block on the disk.
*   **Inode (Index Node):** A data structure that stores metadata for every file or directory on a filesystem (permissions, owner, size, timestamps, addresses of data blocks on disk, etc.). The filename is a reference to the inode number.
*   **Decimal vs. Binary:** Disk manufacturers often specify capacity in decimal (1 KB = 1000 Bytes, 1 MB = 1000 KB), while operating systems usually calculate in binary (1 KiB = 1024 Bytes, 1 MiB = 1024 KiB). This is why a 1 TB disk might appear as approximately 931 GiB in the OS.

##### Partition Tables

Defines the structure for dividing a disk into logical partitions.

*   **MBR (Master Boot Record):** Older standard. Supports a maximum of 4 primary partitions or 3 primary + 1 extended partition. Has a maximum disk size limit of about 2 TB.
*   **GPT (GUID Partition Table):** Modern standard. Supports many more partitions (default 128) and much larger disk sizes (theoretically Zettabytes). Used with UEFI systems.

##### BIOS and UEFI

Firmware systems that initiate and manage the computer's boot process.

*   **BIOS (Basic Input/Output System):** Older system. Initializes hardware, reads the MBR, and executes the bootloader.
*   **UEFI (Unified Extensible Firmware Interface):** Modern system. Offers faster boot times, support for larger disks (with GPT), a more advanced interface, and enhanced security features.

##### Bootloader

The program responsible for loading the operating system kernel into memory and starting it (e.g., GRUB, LILO). Runs after the MBR or GPT. If multiple operating systems are installed, it may present a menu to choose which one to boot.

##### Filesystem

The structure and set of rules that determine how data is organized, stored, accessed, and managed on a disk. After partitioning a disk, each partition must be formatted with a filesystem (`mkfs` command).

*   **Common Linux Filesystems:**
    *   `ext4`: The most widely used, stable, and mature Linux filesystem. Features journaling to protect data integrity.
    *   `XFS`: A high-performance, journaling filesystem optimized for large files and filesystems.
    *   `Btrfs`: A modern, copy-on-write filesystem offering advanced features like snapshots and built-in RAID.
*   **Other Filesystems:** `FAT32`, `exFAT` (for compatibility with USB drives), `NTFS` (for compatibility with Windows).

##### Disk Management Commands

*   `lsblk` (List Block Devices): Lists block devices (disks and partitions) in the system in a tree structure.
    *   `lsblk -f`: Shows additional information like filesystem type, UUID, and mount point.
*   `fdisk`: Used to manage disks with MBR partition tables (create, delete, change partition type). It's an interactive command.
    *   `sudo fdisk -l`: Lists all disks and their partitions.
    *   `sudo fdisk /dev/sda`: Enters interactive mode to operate on the `/dev/sda` disk.
*   `gdisk`: Used to manage disks with GPT partition tables (the GPT equivalent of `fdisk`).
*   `parted`: A more advanced tool capable of managing both MBR and GPT disks. Can be used in both interactive and command-line modes.
*   `mkfs` (Make Filesystem): Creates a filesystem on a disk partition (formats it).
    *   `sudo mkfs.ext4 /dev/sdb1`: Formats the `/dev/sdb1` partition as `ext4`.
    *   `sudo mkfs.xfs /dev/sdb2`: Formats the `/dev/sdb2` partition as `XFS`.
    *   `sudo mkfs -t ntfs /dev/sdc1`: Formats the `/dev/sdc1` partition as `NTFS` (specifying type with `-t`).
*   `mount`: Makes a filesystem (disk partition, USB drive, network share) accessible by attaching it to a specified directory (mount point).
    *   `sudo mount /dev/sdb1 /mnt/data`: Mounts the `/dev/sdb1` partition to the `/mnt/data` directory (the `/mnt/data` directory must exist beforehand).
    *   `mount`: Lists all currently mounted filesystems.
    *   `sudo mount -o remount,rw /dev/sda1`: Remounts `/dev/sda1` in read-write mode.
*   `umount`: Detaches a mounted filesystem.
    *   `sudo umount /mnt/data`: Unmounts the device mounted at `/mnt/data`.
    *   `sudo umount /dev/sdb1`: Can also unmount by device name.
    *   **Note:** No process should be actively using the directory being unmounted (e.g., don't be `cd`'d into it).
*   `/etc/fstab` (File System Table): A file that defines filesystems to be automatically mounted at system boot. Each line defines a filesystem (Device/UUID, Mount Point, Filesystem Type, Mount Options, Dump, Pass). After editing this file, `sudo mount -a` can test/apply the new definitions. Using UUIDs (found with `lsblk -f`) is safer than device names (`/dev/sda1`) which might change.
*   **LVM (Logical Volume Management):** An advanced disk management system that allows pooling physical disks or partitions into a Volume Group (VG) and creating flexible-sized Logical Volumes (LV) from this pool. It simplifies resizing partitions and adding/removing disks. (Detailed topic, should be studied separately).

#### Process Management

*   **What is a Process?** An instance of a running program. While a program is a passive file on disk, when executed, it's loaded into memory and becomes a process. Each process has its own unique identifier (PID - Process ID), memory space, file descriptors, and state (running, sleeping, zombie, etc.).
*   **Process Types:**
    *   **Foreground Processes:** Processes started in the terminal that retain control of the terminal. The terminal doesn't accept new commands until the command finishes or the user intervenes.
    *   **Background Processes:** Processes started from the terminal but release control back to it. Started by appending `&` to the command (`sleep 60 &`).
    *   **Daemons (Services):** Special processes that start at system boot and run continuously in the background, usually without user interaction (e.g., web server, database server).
*   **Job Control:** The shell's (especially Bash, Zsh) ability to manage foreground and background processes (jobs) within the current terminal session.
    *   `jobs`: Lists the jobs in the current session (background and stopped ones).
    *   `fg %job_number`: Brings the specified job to the foreground.
    *   `bg %job_number`: Resumes a stopped job to run in the background.
    *   `Ctrl+Z`: Suspends the foreground job and puts it in the background.
*   **Command Chaining/Grouping:**
    *   `command1 ; command2`: `command2` runs after `command1` finishes (regardless of success or failure).
    *   `command1 && command2`: `command2` runs only if `command1` succeeds (exit code 0).
    *   `command1 || command2`: `command2` runs only if `command1` fails (exit code != 0).
    *   `(command1 ; command2)`: Groups commands to run in a subshell.

##### Monitoring and Managing Processes

*   `ps` (Process Status): Shows a snapshot of the current processes.
    *   `ps aux`: Shows all processes for all users in detailed format (BSD style).
    *   `ps -ef`: Shows all processes in full format (System V style).
    *   `ps -ejH`: Shows processes in a tree structure.
    *   `ps -p PID`: Shows information for the process with the specified PID.
    *   `pgrep process_name`: Lists the PIDs of processes matching the given name.
*   `top`: An interactive tool that displays system processes in real-time, sorted by CPU or memory usage. `Shift+M` sorts by memory, `Shift+P` sorts by CPU, `k` can kill a process, `q` quits.
*   `htop`: Similar to `top` but more user-friendly, with color, mouse support, and an interactive interface (usually needs to be installed separately).
*   `kill`: Sends signals to processes to manage them (most commonly to terminate).
    *   `kill PID`: Sends the default TERM (terminate - 15) signal to the process (asks it to shut down gracefully).
    *   `kill -9 PID`: Sends the KILL (9) signal to the process (forces termination, may cause data loss, use as a last resort).
    *   `kill -l`: Lists all available signals (e.g., HUP (1), INT (2), STOP (19), CONT (18)).
*   `pkill process_name`: Sends a signal to all processes matching the given name. `pkill -9 firefox`
*   `killall process_name`: Works like `pkill` but usually matches the exact process name. `killall -9 sleep`
*   `tmux` (Terminal Multiplexer): A tool that allows creating and managing multiple independent terminal sessions (windows, panes) within a single terminal window. Especially useful for SSH connections, as sessions and running processes persist in the background even if the connection drops. Sessions can be reattached later. (Detailed topic, should be studied separately).

#### Service Management (systemd)

On most modern Linux distributions, `systemd` is the system and service manager that handles the boot process (init) and manages services (daemons).

*   **Unit:** Resources managed by `systemd` (services `.service`, mount points `.mount`, devices `.device`, targets `.target`, etc.).
*   `systemctl`: The main command used to control `systemd`. Requires `sudo`.
    *   `systemctl status service_name.service` (or just `service_name`): Shows the status of the service (active, inactive, failed, recent logs). `systemctl status sshd`
    *   `systemctl start service_name`: Starts the service.
    *   `systemctl stop service_name`: Stops the service.
    *   `systemctl restart service_name`: Restarts the service.
    *   `systemctl reload service_name`: Reloads the service's configuration files without stopping the service (if supported).
    *   `systemctl enable service_name`: Enables the service to start automatically at system boot.
    *   `systemctl disable service_name`: Disables the service from starting automatically at system boot.
    *   `systemctl is-enabled service_name`: Checks if the service is enabled to start at boot.
    *   `systemctl list-units --type=service --all`: Lists all service units (active and inactive).
    *   `systemctl list-unit-files --type=service`: Lists all available service files and their states (enabled, disabled, static).

#### Log Management

Files where events occurring on the system (errors, warnings, informational messages, user logins, service activities) are recorded. Critical for troubleshooting and system analysis.

*   **Traditional Logging (syslog):**
    *   Log files are typically stored as plain text in the `/var/log` directory.
    *   Services like `rsyslogd` or `syslog-ng` collect log messages and write them to the appropriate files.
    *   **Important Log Files:**
        *   `/var/log/syslog` or `/var/log/messages`: General system messages.
        *   `/var/log/auth.log` or `/var/log/secure`: Authentication and authorization logs (login attempts, `sudo` usage).
        *   `/var/log/kern.log`: Kernel logs.
        *   `/var/log/boot.log`: System boot logs.
        *   `/var/log/apt/` (Debian/Ubuntu): `apt` package manager logs.
        *   `/var/log/yum.log` or `/var/log/dnf.log` (Red Hat/Fedora): `yum`/`dnf` logs.
        *   Application-specific logs (e.g., `/var/log/nginx/`, `/var/log/apache2/`, `/var/log/mysql/`).
*   **systemd Journal:**
    *   On systems using `systemd`, logs are collected centrally in a structured binary format by the `journald` service.
    *   `journalctl`: Used to view and query the journal logs.
        *   `journalctl`: Shows all logs (newest first).
        *   `journalctl -n 20`: Shows the last 20 log entries.
        *   `journalctl -f`: Follows new logs in real-time.
        *   `journalctl -u service_name.service`: Shows logs for the specified service. `journalctl -u sshd`
        *   `journalctl --since "1 hour ago"`: Shows logs from the last hour. (`"YYYY-MM-DD HH:MM:SS"` format can also be used).
        *   `journalctl -p err`: Shows only error level logs (`emerg`, `alert`, `crit`, `err`, `warning`, `notice`, `info`, `debug`).
        *   `journalctl _PID=1234`: Shows logs for the specified PID.
*   **Log Rotation:** A mechanism to prevent log files from growing too large over time by archiving or deleting old logs. Usually managed by the `logrotate` tool (`/etc/logrotate.conf` and `/etc/logrotate.d/`).

#### Basic Network Concepts and Commands

##### Network Basics

*   **IP Address (Internet Protocol Address):** A logical address that uniquely identifies a device on a network (e.g., `192.168.1.10`, `2001:0db8:85a3::8a2e:0370:7334`). Comes in IPv4 (32-bit) and IPv6 (128-bit) versions.
*   **MAC Address (Media Access Control Address):** The physically unique address assigned to a network interface card (Ethernet, Wi-Fi) at the hardware level (e.g., `0A:1B:2C:3D:4E:5F`). Used at Layer 2 (Data Link Layer).
*   **LAN (Local Area Network):** A network connecting devices within the same physical network segment (typically within the same building or home).
*   **WAN (Wide Area Network):** A network connecting LANs across different geographical locations (the Internet is the largest WAN).
*   **Router:** A device that connects different networks and directs packets between them to the correct destination. Operates based on IP addresses (Layer 3). Uses routing tables.
*   **Switch:** A device that connects devices within the same LAN. Operates based on MAC addresses (Layer 2). Optimizes network traffic by sending packets only to the relevant port.
*   **Gateway:** The IP address of the router that serves as the exit point from one network to another (usually from a LAN to the Internet).
*   **DNS (Domain Name System):** A distributed system that translates human-readable domain names (`www.google.com`) into computer-understandable IP addresses (`172.217.160.142`).
*   **DHCP (Dynamic Host Configuration Protocol):** A protocol that automatically assigns IP addresses, subnet masks, gateway addresses, and DNS server information to devices on a network.

##### How Hosts Communicate

*   **Within the Same LAN:**
    1.  The source device knows the target device's IP address but not its MAC address.
    2.  The source sends an ARP (Address Resolution Protocol) request to the LAN: "What is the MAC address of the device with this IP?"
    3.  The device with the target IP address responds with an ARP reply containing its MAC address.
    4.  The source device caches the target MAC address in its ARP table.
    5.  Communication now occurs directly from source MAC to destination MAC (via the Switch).
*   **Between Different LANs (Via Router):**
    1.  The source device determines that the destination IP address is not on its own LAN.
    2.  It sends the packet to the MAC address of its configured gateway (router) (learning the router's MAC via ARP). The destination IP address inside the packet remains unchanged.
    3.  The router receives the packet, looks at the destination IP address, and consults its routing table to forward the packet to the next router or directly to the destination LAN. During this, the packet's source MAC address is updated to the router's MAC, and the destination MAC address is updated to the MAC of the next hop (router or destination device).
    4.  This process repeats until the packet reaches the destination network. The final router sends the packet to the destination device's MAC address.
*   **Over the Internet (e.g., www.google.com):**
    1.  Your device queries its DNS server for the IP address of `www.google.com`.
    2.  DNS returns an IP address belonging to Google's servers (often a Load Balancer/Edge Router).
    3.  Your device sends the packet towards this destination IP address to its gateway (router).
    4.  The packet traverses multiple routers across the Internet to reach Google's network.
    5.  Google's Load Balancer receives the request and directs it to an appropriate backend server. This internal mechanism is hidden from the outside.

##### Network Protocols (Summary)

*   **ARP:** IP -> MAC resolution (within LAN).
*   **IP:** Logical addressing and routing (Network Layer).
*   **TCP (Transmission Control Protocol):** Reliable, connection-oriented data transmission (Transport Layer - HTTP, FTP, SMTP).
*   **UDP (User Datagram Protocol):** Fast, connectionless data transmission (Transport Layer - DNS, DHCP, VoIP).
*   **ICMP (Internet Control Message Protocol):** Used for network status and error messages (`ping`, `traceroute`).
*   **HTTP/HTTPS:** Web page transfer (Application Layer).
*   **FTP:** File transfer (Application Layer).
*   **SMTP:** Email sending (Application Layer).
*   **POP3/IMAP:** Email retrieval (Application Layer).
*   **SSH:** Secure remote command execution and file transfer (Application Layer).
*   **DNS:** Domain name -> IP resolution (Application Layer).
*   **DHCP:** Automatic IP configuration (Application Layer).

##### Basic Network Commands

*   `ping target_ip_or_domain`: Tests reachability and response time to a target host by sending ICMP echo requests. `ping google.com` or `ping 8.8.8.8`. Stop with `Ctrl+C`.
*   `ip`: A modern and powerful tool for managing network interfaces, IP addresses, routing tables, and the ARP cache (replaces `ifconfig`, `route`, `arp`).
    *   `ip addr show` (or `ip a`): Lists all network interfaces and their assigned IP addresses.
    *   `ip link show`: Shows link-layer information for network interfaces (MAC address, status: UP/DOWN).
    *   `sudo ip link set eth0 up/down`: Enables/disables the specified interface.
    *   `ip route show` (or `ip r`): Shows the IP routing table (which networks are reachable via which interface and gateway).
    *   `ip neigh show`: Shows the neighbor table (ARP cache - IP/MAC mappings).
*   `ifconfig`: (Legacy) Lists/configures network interfaces and IP addresses. The `ip` command is preferred on modern systems.
*   `route`: (Legacy) Shows/manages the IP routing table. `ip route` is preferred.
*   `arp`: (Legacy) Shows/manages the ARP cache. `ip neigh` is preferred. `arp -a`
*   `hostname`: Shows or sets the system's hostname.
    *   `hostname`: Shows the current name.
    *   `hostname -I`: Shows all IP addresses of the system.
*   `nslookup domain_name [dns_server]`: Queries the IP address for a domain name. `nslookup google.com`
*   `dig domain_name [type] [@dns_server]`: A more detailed and flexible tool for making DNS queries.
    *   `dig google.com`: Queries the A record (IPv4 address).
    *   `dig google.com MX`: Queries the MX record (mail server).
    *   `dig google.com AAAA`: Queries the AAAA record (IPv6 address).
    *   `dig @8.8.8.8 google.com`: Queries the specified DNS server.
*   `traceroute domain_or_ip` (or `tracepath`): Attempts to show the routers (hops) a packet passes through to reach a destination, along with latency times. Used to find network slowdown points.
*   `ss` (Socket Statistics): Shows active network connections, listening ports, and socket statistics (the modern replacement for `netstat`).
    *   `ss -tulnp`: Shows all listening TCP (`t`) and UDP (`u`) ports, with port numbers (`n`) and the associated process (`p`) (usually requires `sudo`).
    *   `ss -tan`: Shows all TCP connections.
*   `netstat`: (Legacy) Shows network connections, routing tables, interface statistics, etc. `ss` and `ip` commands are preferred.
*   `wget url`: Downloads files from the specified URL. `wget https://example.com/file.zip`
*   `curl url`: A versatile tool for transferring data from or to a URL. Can download web pages, interact with APIs, upload/download files, etc. `curl https://example.com` (prints the page's HTML content to the screen). `curl -O url` downloads the file (like `wget`).
*   `ssh user@target_ip_or_domain`: Establishes a secure shell connection to a remote Linux/Unix server.
*   `scp source_file user@target_ip:target_path`: Securely copies files over SSH (Secure Copy). To get files from remote: `scp user@target_ip:source_file local_target`
*   `nmtui`: (If NetworkManager is installed) Provides a text-based user interface for configuring network connections (IP settings, Wi-Fi, Ethernet). Changes are persistent.
*   `tcpdump`: A powerful command-line packet analyzer. Captures packets passing through a network interface for detailed inspection. Often used for in-depth network troubleshooting (requires `sudo`). `sudo tcpdump -i eth0`
*   `nmap`: A popular tool for network discovery and security auditing. Used to find active devices, open ports, and running services on a network (usually needs to be installed separately).
    *   `nmap target_ip`: Scans common ports on the target IP.
    *   `nmap -sn 192.168.1.0/24`: Attempts to find active hosts on the local network (ping scan).
    *   `nmap -p 1-1000 target_ip`: Scans the first 1000 ports on the target.
*   `/etc/hosts`: A local DNS resolution file. IP-Hostname mappings added here are used before querying a DNS server. Can be used to block specific sites or define domain names for local development environments.
*   `/etc/resolv.conf`: Contains the addresses of the DNS servers the system should use. Often managed automatically by NetworkManager or DHCP.
