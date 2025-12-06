# LINUX

## Basics
- OS is: KERNEL + GNU (Software/Packages)
- Features of Linux:
  - Open source
  - secure
  - light weight
  - simplified updates
  - multiple distribution versions

## Some useful Linux Commands & Utilities

### `cat` Command  
The `cat` command is a universal tool used to copy standard input to standard output. It is mainly used for:  
- Creating files  
- Viewing file contents  
- Concatenating multiple files  
- Copying content from one file to another  
- Reversing file content (using `tac`)  
- **Cannot edit** a file, only view or append content.  
- **`>`**: Redirects output to overwrite a file.  
- **`>>`**: Appends content to an existing file.  

**It's common Commands**:
#### Create a File  
```bash
cat > file-name
# Type the content
# Press Ctrl+D to save
```

#### Read/View a File  
```bash
cat file-name
```

#### Append Content to an Existing File  
```bash
cat >> file-name
# Type new content
# Press Ctrl+D to save
```

#### Concatenate Two Files and Save to a Third  
```bash
cat file-1 file-2 > file-3
```

#### Reverse a File (Using `tac`)  
```bash
tac file-name
```

#### Copy Content of One File to Another  
```bash
cat file-1 > file-2
```

#### Additional Options:  
- `cat -b` → Number only non-blank lines  
- `cat -s` → Squeeze multiple blank lines into one  
- `cat -n` → Number all lines  
- `cat -E` → Display `$` at the end of each line  


### `touch` Command  
The `touch` command is used for:  
- Creating empty files  
- Creating multiple empty files  
- Updating file timestamps  
- Modifying access and modification times  
- Timestamp Modifications:  
  - `touch -a` → Updates last access time  
  - `touch -m` → Updates last modification time  

**It's Common Commands**:  
#### Create a Single File  
```bash
touch file-name
```

#### Create Multiple Files  
```bash
touch file-1 file-2 file-3
```

#### Check File Timestamp  
```bash
stat file-name
```

#### Change Access Time  
```bash
touch -a file-name
```

#### Change Modification Time  
```bash
touch -m file-name
```


### VI Editor (`vi`)  
The `vi` editor is a powerful text editor used in Linux.

#### Create or Open a File  
```bash
vi file-name
```

#### Steps to Edit and Save  
1. Press `i` → Enter **INSERT** mode.  
2. Type the content.  
3. Press `ESC` → Exit **INSERT** mode.  
4. Use the following commands:  
   - `:w` → Save the file.  
   - `:wq` or `:x` → Save and quit.  
   - `:q` → Quit (only if no changes were made).  
   - `:q!` → Quit **forcefully** without saving.  


### Important `ls` Commands  
The `ls` command is used to list files and directories.

| Command | Description |
|---------|------------|
| `ls` | List files and directories in the current directory. |
| `ls -l` | List with detailed information (permissions, size, owner, etc.). |
| `ls -a` | Show **hidden** files (files starting with `.`). |
| `ls -lh` | Display file sizes in **human-readable** format. |
| `ls -lt` | Sort files by **modification time** (latest first). |
| `ls -R` | Recursively list all **subdirectories**. |


### Important File Commands  
| Command | Description |
|---------|------------|
| `touch file-name` | Create a new empty file. |
| `cat file-name` | View file content. |
| `nano file-name` | Open file in **Nano** editor. |
| `rm file-name` | Delete a file. |
| `mv old-name new-name` | Rename or move a file. |
| `cp source destination` | Copy a file. |


### Important Directory Commands  
| Command | Description |
|---------|------------|
| `mkdir dir-name` | Create a directory. |
| `rmdir dir-name` | Remove an **empty** directory. |
| `rm -r dir-name` | Remove a directory **and its contents**. |
| `cd dir-name` | Change into a directory. |
| `cd ..` | Move **up** one level. |
| `pwd` | Show the **current directory path**. |


### Cut, Copy, Paste, Remove Commands  

| Command | Description |
|---------|------------|
| `cp source destination` | Copy a file. |
| `cp -r source destination` | Copy a **directory** (with contents). |
| `mv old-name new-name` | Move or **rename** a file/directory. |
| `rm file-name` | Remove a file. |
| `rm -r dir-name` | Remove a directory **and its contents**. |
| `rm -i file-name` | Remove a file **with confirmation**. |
| `rm -f file-name` | Force remove a file **without confirmation**. |


### Important `cd` Commands  

| Command | Description |
|---------|------------|
| `cd dir-name` | Change into a specific directory. |
| `cd ..` | Move **up** one level. |
| `cd ~` or `cd` | Go to the **home directory**. |
| `cd /` | Go to the **root directory**. |
| `cd -` | Switch to the **previous directory**. |


### Important `grep` Commands  
The `grep` command is used to **search for patterns** in files.  

| Command | Description |
|---------|------------|
| `grep "text" file.txt` | Find `"text"` in `file.txt`. |
| `grep -i "text" file.txt` | Case-insensitive search. |
| `grep -r "text" directory/` | Recursively search in a directory. |
| `grep -n "text" file.txt` | Show **line numbers** with matches. |
| `grep -v "text" file.txt` | Show lines **without** the pattern. |
| `grep -c "text" file.txt` | Count the number of matches. |


### Important Process Commands  
| Command | Description |
|---------|------------|
| `ps aux` | Show all running processes. |
| `top` | Display active processes and resource usage. |
| `htop` | Interactive process viewer (if installed). |
| `kill PID` | Kill a process by **PID** (Process ID). |
| `kill -9 PID` | Forcefully kill a process. |
| `pkill process-name` | Kill a process by **name**. |
| `bg` | Resume a **stopped** process in the background. |
| `fg` | Bring a **background** process to the foreground. |
| `jobs` | List background jobs. |

### Important SSH Commands  
| Command | Description |
|---------|------------|
| `ssh user@host` | Connect to a remote machine via SSH. |
| `ssh -p port user@host` | Connect using a **specific port**. |
| `scp file user@host:/path` | Securely copy a file to a remote server. |
| `scp user@host:/path/file .` | Download a file from a remote server. |
| `rsync -avz file user@host:/path` | Sync files between local and remote. |
| `ssh-keygen` | Generate an SSH key pair. |
| `ssh-copy-id user@host` | Copy SSH key to a remote server for passwordless login. |

### Important Networking Commands  
| Command | Description |
|---------|------------|
| `ifconfig` / `ip a` | Display network interfaces and IPs. |
| `ping host` | Test network connectivity. |
| `traceroute host` | Trace the path packets take to a host. |
| `netstat -tulnp` | Show open ports and active connections. |
| `ss -tulnp` | More efficient alternative to `netstat`. |
| `nslookup domain` | Get DNS information for a domain. |
| `dig domain` | Get detailed DNS records. |
| `curl -I URL` | Fetch only headers from a website. |
| `wget URL` | Download a file from a URL. |

### Important User Commands  
| Command | Description |
|---------|------------|
| `whoami` | Show the current user. |
| `who` | List logged-in users. |
| `id` | Display **user ID (UID)** and **group ID (GID)**. |
| `adduser username` / `useradd username` | Create a new user. |
| `passwd username` | Change a user's password. |
| `deluser username` / `userdel username` | Delete a user. |
| `groupadd groupname` | Create a new group. |
| `usermod -aG groupname username` | Add a user to a group. |
| `groups username` | Show a user's group memberships. |


### `tar`, `gzip`, `zip`, `wget`, etc. Commands  
| Command | Description |
|---------|------------|
| `tar -cvf archive.tar file` | Create a `.tar` archive. |
| `tar -xvf archive.tar` | Extract a `.tar` archive. |
| `tar -cvzf archive.tar.gz file` | Create a **compressed** `.tar.gz` archive. |
| `tar -xvzf archive.tar.gz` | Extract a `.tar.gz` archive. |
| `zip archive.zip file` | Create a `.zip` archive. |
| `unzip archive.zip` | Extract a `.zip` file. |
| `gzip file` | Compress a file using `.gz`. |
| `gunzip file.gz` | Decompress a `.gz` file. |
| `wget URL` | Download a file from a URL. |
| `wget -c URL` | Resume an interrupted download. |


### Access Modes and Permissions  

#### File Permission Representation  
Each file has **three permission groups**:  
- **Owner (User)**  
- **Group**  
- **Others (World)**  

Each group has **three permission types**:  
| Symbol | Permission | Numeric Value |
|--------|-----------|---------------|
| `r` | Read | 4 |
| `w` | Write | 2 |
| `x` | Execute | 1 |

**Example**:  
```bash
-rwxr-xr-- 1 user group 1234 Mar 20 10:00 file.txt
```
- `rwx` → **Owner** has **read, write, execute** permissions.
- `r-x` → **Group** has **read, execute** permissions.
- `r--` → **Others** have **read-only** permission.

#### Changing Permissions  
| Command | Description |
|---------|------------|
| `chmod 755 file` | Change permissions using numeric mode (`rwxr-xr-x`). |
| `chmod u+x file` | Add execute permission for the owner. |
| `chmod g-w file` | Remove write permission for the group. |
| `chmod o=r file` | Set **read-only** for others. |

#### Changing Ownership  
| Command | Description |
|---------|------------|
| `chown user file` | Change file **owner**. |
| `chown user:group file` | Change file **owner and group**. |
| `chgrp group file` | Change **group ownership**. |


### Kernel Information 
- Navigate to the boot directory:  
  ```bash
  cd /boot/
  ls   # The last file is the kernel
  ```
- Alternatively, use:  
  ```bash
  uname  # Displays system information
  ```

### Command Documentation  
- To know more about a command:  
  ```bash
  man <command>
  ```  

### Text Processing  
- **`tr` (Translate text)**  
  Example: Convert `file.txt` content to uppercase and store it in `upper.txt`:  
  ```bash
  cat file.txt | tr a-z A-Z > upper.txt
  ```
- **`\` (Backslash for multiline commands)**  
  Example:  
  ```bash
  echo "This is a long command that" \
  " continues on the next line"
  ```

### Disk Management
- **Check disk space:**  
  ```bash
  df
  ```
- **Check disk usage stats:**  
  ```bash
  du
  ```
  - **Note:**  
    - `df` (Disk Free) fetches data from filesystem metadata → **faster**  
    - `du` (Disk Usage) scans disk blocks → **detailed but slower**  

### File Operations
- **View specific lines of a file:**  
  ```bash
  head -n 2 data.txt   # View first 2 lines
  tail -n 4 data.txt   # View last 4 lines
  ```

- **Find files and directories:**  
  - Using `locate`:  
    ```bash
    locate file.txt   # Find a specific file  
    locate "*.txt"    # Find all text files  
    ```
  - Using `find`:  
    ```bash
    find . -type d                # Find directories in the current directory  
    find . -type f -name "*.txt"   # Find all .txt files  
    find . -type f -mmin +2 -mmin -10  # Find files modified between 2 to 10 mins ago  
    ```
  - **Important `find` flags:**  
    ```
    -maxdepth : Limit search depth  
    -size     : Filter by file size  
    -empty    : Show empty files  
    -perm     : Filter by file permissions  
    ```

### Command History & User Managemen
- **Run previous commands:**  
  ```bash
  !command-name   # Run last command with the same name  
  !command-number # Run a specific command from history  
  ```
- **User management:**  
  ```bash
  useradd <User>      # Add a new user  
  passwd <User>       # Set user password  
  userdel <User>      # Delete user  
  ```

### System Information & Monitoring  
| **Command**  | **Description**  |
|-------------|-----------------|
| `uname`     | OS name         |
| `uname -o`  | OS type         |
| `uname -m`  | System architecture |
| `uname -r`  | Kernel version  |
| `lscpu`     | CPU details     |
| `vmstat`    | Virtual memory stats |
| `id`        | User's group IDs |
| `lsof`      | List open files |
| `netstat`   | List active listening ports |
| `ps aux`    | List running processes & resource usage |

- **Breakdown of `ps aux`:**  
  - `a` → Show processes for all users  
  - `u` → Display process owner  
  - `x` → Show processes not attached to a terminal  

### Operators & Command Chaining  
| **Operator**  | **Description**  |
|--------------|-----------------|
| `&&`         | Run second command **only if** the first succeeds |
| `>>`         | Append output to a file |
| `||`         | Run second command **only if** the first fails |

- **Example:**  
  ```bash
  echo "hi" && { echo "second"; echo "third"; }
  ```



## Linux Redirects 
**Redirects** in Linux allow you to manage input/output streams when running commands, such as storing output or errors in files.  

### Types of Redirects
1. **stdin (0)** - Standard input (keyboard input).
   - Redirect input from a file:  
     ```bash
     command < file.txt
     ```

2. **stdout (1)** - Standard output (normal output of commands).
   - Redirect output to a file:  
     ```bash
     command > output.txt  # Overwrites file
     command >> output.txt # Appends to file
     ```

3. **stderr (2)** - Standard error (error messages).
   - Redirect errors to a file:  
     ```bash
     command 2> errors.txt
     ```

### Combining stdout and stderr
- Redirect both to the same file:  
  ```bash
  command > all_output.txt 2>&1
  ```




## File System
- A method used by OS to store, retrieve, and manage files on storage devices like hard drives, SSDs, and USBs.
- Determines how data is structured, named, and accessed.   

**Types of File Systems**
| File System | Features |
|------------|----------|
| **ext3 (Third Extended File System)** | Introduced journaling (keeps track of changes for recovery) |
| **ext4 (Fourth Extended File System)** | Supports large files (16TB) and better performance than ext3 |
| **XFS** | High-performance journaling file system, good for large-scale storage |
| **BtrFS (B-Tree File System)** | Supports snapshots, checksums, and self-healing |
| **FAT (File Allocation Table)** | Used in USB drives, widely compatible but lacks journaling |

- Distributions usage:
  - **Ubuntu, Debian**: ext4 (default)  
  - **Red Hat Enterprise Linux (RHEL), CentOS, Fedora**: XFS (default) but supports ext4  
  - **SUSE Linux Enterprise**: BtrFS (default)  
  - **Arch Linux, Manjaro**: ext4 (default) 


### Inode
- **inode (Index Node)** is a data structure in Linux that stores metadata about a file, such as:  
  - File type (regular file, directory, etc.)  
  - Permissions (read, write, execute)  
  - Owner and group  
  - File size  
  - Timestamps (created, modified, accessed)  
  - Pointer to actual file data  

> Fun fact: Inodes do NOT store file names! The directory structure maps file names to inodes.


**Important Files in Linux**:
| File | Purpose |
|------|---------|
| `/etc/fstab` | Lists disk partitions and mount points |
| `/etc/mtab` | Shows currently mounted file systems |
| `/var/log/` | Stores system logs |
| `/boot/` | Contains boot-related files like kernels |
| `/home/` | Stores user directories |
| `/dev/` | Contains device files (e.g., USB, HDD) |

### Types of Files in Linux 
| File Type | Code | Description |
|-----------|------|-------------|
| **Regular File** | `-` | Normal files (text, binary, etc.) |
| **Directory** | `d` | Folders that contain files |
| **Symbolic Link** | `l` | Shortcut to another file |
| **Character Device** | `c` | Hardware devices (keyboard, mouse, etc.) |
| **Block Device** | `b` | Storage devices (HDD, USB, etc.) |
| **Socket** | `s` | Network communication endpoint |
| **Named Pipe** | `p` | Used for inter-process communication (IPC) |



## Cron Jobs & Crontab
- **cron** is a system service used to schedule and automate tasks (called **cron jobs**) at specific times or intervals. Runs in the background and executes commands or scripts without user intervention.  
- `crontab` (short for **cron table**) is a file where you define scheduled jobs. Each user can have their own crontab file.  

**Useful Commands**:  
| Command | Description |
|---------|------------|
| `crontab -l` | List current cron jobs |
| `crontab -e` | Edit cron jobs |
| `crontab -r` | Remove all cron jobs |

### Crontab Syntax 
A cron job has 5 time fields + 1 command:  
```bash
MIN HOUR DOM MON DOW COMMAND
```
| Field | Allowed Values | Description |
|--------|---------------|-------------|
| **MIN** | 0-59 | Minute of the hour |
| **HOUR** | 0-23 | Hour of the day |
| **DOM (Day of Month)** | 1-31 | Day of the month |
| **MON (Month)** | 1-12 | Month (1 = January, 12 = December) |
| **DOW (Day of Week)** | 0-6 | Day of the week (0 = Sunday, 6 = Saturday) |
| **COMMAND** | Any shell command | The task to execute |

**Example**:  
```bash
30 14 * * 1 echo "Hello, World!" >> ~/cron_log.txt
```
Runs at **2:30 PM every Monday** and appends "Hello, World!" to a file.

### Common Cron Job Examples  
| Schedule | Cron Expression | Example Task |
|-----------|----------------|--------------|
| Every Minute | `* * * * *` | Run a script every minute |
| Every 5 Minutes | `*/5 * * * *` | Run every 5 minutes |
| Every Hour | `0 * * * *` | Run at the start of every hour |
| Every Day at 3 AM | `0 3 * * *` | Run daily at 3 AM |
| Every Sunday at 1 PM | `0 13 * * 0` | Run every Sunday at 1 PM |
| Every First Day of the Month | `0 0 1 * *` | Run on the 1st of every month |


### Special Cron Keywords  
| Keyword | Equivalent |
|---------|-----------|
| `@reboot` | Runs once at startup |
| `@hourly` | Runs every hour (`0 * * * *`) |
| `@daily` | Runs every day at midnight (`0 0 * * *`) |
| `@weekly` | Runs every Sunday at midnight (`0 0 * * 0`) |
| `@monthly` | Runs on the first day of the month (`0 0 1 * *`) |
| `@yearly` | Runs once a year (`0 0 1 1 *`) |

**Example**:  
```bash
@daily /home/user/backup.sh
```
Runs the **backup.sh** script every day at midnight.


### Redirecting Output & Debugging  
By default, cron jobs do not show output. Use redirection to log output:  

```bash
0 0 * * * /path/to/script.sh >> /var/log/mycron.log 2>&1
```
- `>> /var/log/mycron.log` → Saves output to a log file  
- `2>&1` → Captures errors  



## Update vs Upgrade in Linux
Both `update` and `upgrade` are used for package management. 

| Action | Command | Description |
|--------|--------|-------------|
| **Update** | `sudo apt update` | Fetches the latest package lists from repositories but does **not** install anything. |
| **Upgrade** | `sudo apt upgrade` | Installs newer versions of installed packages while keeping configurations. |
| **Dist-Upgrade** | `sudo apt full-upgrade` | Upgrades packages **with dependencies** and may remove old ones. |

**Example**: 
```bash
sudo apt update && sudo apt upgrade -y
```


## SUID and SGID
They are **special file permissions** in Linux that change how files and programs execute.  

### SUID (Set User ID)
- When a file has **SUID**, it runs **as the file owner** instead of the user who executes it.  
- Commonly used in **system binaries** like `passwd`.  

#### Commands
- Checking SUID: `ls -l /usr/bin/passwd`
  - Output: `-rwsr-xr-x 1 root root 54256 Jan  1 12:00 /usr/bin/passwd`
  - The `s` in `-rws` means **SUID is set** (instead of `x`).  
- Set SUID on a file: `chmod u+s filename`
- Remove SUID: `chmod u-s filename`


### SGID (Set Group ID)
- When a file has **SGID**, it runs **as the file’s group owner** instead of the user.  
- Useful in **shared directories** where all users need the same permissions.  

#### Commands:
- Checking SGID: `ls -l /usr/bin/write`
  - Output: `-rwxr-sr-x 1 root tty 31032 Jan  1 12:00 /usr/bin/write`
  - The `s` in `r-s` means **SGID is set**
- Set SGID on a file: `chmod g+s filename`
- Remove SGID: `chmod g-s filename`


## Sticky Bit (Restricted Deletion Flag)  
- A **special permission** used on directories to **prevent users from deleting files they don’t own**.  
- Commonly applied to **/tmp**, where multiple users can create files, but only the **owner** or `root` can delete them.  

### Commands: 
- Checking Sticky Bit: `ls -ld /tmp` 
  - Output: `drwxrwxrwt 10 root root 4096 Mar 18 12:00 /tmp`
  - The `t` at the end (`rwt`) means **Sticky Bit is set**.
- Set Sticky Bit on a directory: `chmod +t directory_name`
- Remove Sticky Bit: `chmod -t directory_name`



## Logrotate
- A system utility that **automates log file management** by:  
  - Rotating logs (creating new ones)  
  - Compressing old logs  
  - Deleting or archiving logs after a certain period  
- Prevents logs from consuming too much disk space  
- Helps in debugging by keeping logs organized  
- Automates log management without manual intervention 
- Check if Logrotate is Installed: `logrotate --version`  
- Logrotate Configuration File:
  - Located at: **`/etc/logrotate.conf`** (global settings)  
  - Custom configurations can be placed in: **`/etc/logrotate.d/`**  


**Basic Logrotate Configuration Example**:
```bash
/var/log/nginx/*.log {
    daily
    rotate 7
    compress
    missingok
    notifempty
    delaycompress
    postrotate
        systemctl reload nginx
    endscript
}
```
**Explanation**:  
- `daily` → Rotate logs every day  
- `rotate 7` → Keep logs for **7 days**, then delete old ones  
- `compress` → Compress older logs to save space  
- `missingok` → Ignore errors if log files are missing  
- `notifempty` → Don't rotate empty logs  
- `delaycompress` → Compress logs **one day after rotation**  
- `postrotate` → Restart service after rotating logs  



## rsync vs Normal File Transfer
Both **rsync** and normal file transfer methods like **scp** (Secure Copy) and **cp** (Copy) are used to move files between servers.  

| Feature      | rsync | Normal File Transfer (scp, cp) |
|-------------|--------|------------------------------|
| **Speed** | Faster (copies only differences) | Slower (copies entire file every time) |
| **Efficiency** | Uses delta transfer (only modified parts) | Always transfers full file |
| **Resume Support** | Yes (can resume interrupted transfers) | No (must restart from beginning) |
| **Bandwidth Usage** | Less (compresses and syncs data) | More (copies entire file again) |
| **Preserves Permissions & Ownership** | Yes | Sometimes (depends on command used) |
| **Uses SSH?** | Yes | Yes (for scp) |

When to use **rsync**?
- When transferring **large files** over the network.  
- When needing **incremental updates**.  
- When transferring **directories with multiple sub-files**. 
  
When to use **scp/cp**?  
- When transferring **one-time** files.  
- When **rsync** is not installed.  
- When speed and bandwidth don’t matter.  

### rsync Commands: 
- Basic rsync usage: `rsync -av source_file_or_directory destination`
  - `-a` → Archive mode (preserves permissions, timestamps, symbolic links)  
  - `-v` → Verbose mode (shows progress)  
- Sync a local folder to a remote server: `rsync -av /local/path/ user@remote:/remote/path/`
- Sync and delete files that are not in the source anymore: `rsync -av --delete /local/path/ user@remote:/remote/path/`  
- Resume an interrupted transfer: `rsync --partial --progress source_file user@remote:/destination/`  


### Normal File Transfer (`scp` & `cp` Commands)
- Using `scp` (Secure Copy) to copy files to a remote server: `scp local_file user@remote:/remote/directory/`  
- Using `scp` to copy a directory recursively: `scp -r local_directory/ user@remote:/remote/directory/`  
- Using `cp` to copy files locally: `cp source_file destination_directory/` 


## FTP 
- FTP (File Transfer Protocol) is used for transferring files between a **client and a server**. 
- Unlike **scp** or **rsync**, FTP is **not secure** by default.  

**When to use FTP?**  
- For hosting **web files** on a remote server.  
- For **public file sharing** without security concerns.  
- When interacting with **legacy servers**. 

### Setting Up an FTP Server
1. Step 1: Install an FTP server **(vsftpd - Very Secure FTP Daemon)** 
    ```bash
    sudo apt update
    sudo apt install vsftpd
    ```
2. Step 2: Start the FTP Service  
    ```bash
    sudo systemctl start vsftpd
    sudo systemctl enable vsftpd
    ```
3. Step 3: Configure FTP (Edit `vsftpd.conf`)
    ```bash
    sudo nano /etc/vsftpd.conf
    ```
4. Step 4: Restart the FTP Service
    ```bash
    sudo systemctl restart vsftpd
    ```

### FTP Client Commands
- Connect to an FTP server: `ftp server-ip`
- Login as a user:
    ```bash
    Name: your-username
    Password: your-password
    ```
- Download a file from the FTP server: `get filename`
- Upload a file to the FTP server: `put filename`

 


## NFS
NFS (Network File System) allows **file sharing** between multiple Linux systems **over a network**.  


### Setting Up an NFS Server
1. Step 1: Install NFS Server  
    ```bash
    sudo apt update
    sudo apt install nfs-kernel-server
    ```
2. Step 2: Create a Shared Directory: `sudo mkdir -p /mnt/nfs_share` 
3. Step 3: Set Permissions: `sudo chmod 777 /mnt/nfs_share`
4. Step 4: Add the Directory to the NFS Export File:  
  1. Edit the exports file:
      ```bash
      sudo nano /etc/exports
      ```
  2. Add the following line:
      ```bash
      /mnt/nfs_share *(rw,sync,no_root_squash,no_subtree_check)
      ```
5. Step 5: Restart NFS Service: `sudo systemctl restart nfs-kernel-server` 


### Setting Up an NFS Client
1. Step 1: Install NFS Client: `sudo apt install nfs-common` 
2. Step 2: Create a Mount Point: `sudo mkdir -p /mnt/nfs_client`
3. Step 3: Mount the NFS Share: `sudo mount server-ip:/mnt/nfs_share /mnt/nfs_client`  
4. Step 4: Verify the Mounted Share:
    ```bash
    df -h
    ls /mnt/nfs_client
    ```
  - To Make the Mount Permanent (Add to `/etc/fstab`) 
    ```bash
    server-ip:/mnt/nfs_share /mnt/nfs_client nfs defaults 0 0
    ```


## Hard Link vs Soft Link in Linux
In Linux, both **hard links** and **soft links (symbolic links)** are used to create references to a file, but they function differently.

| Feature       | Hard Link | Soft Link (Symbolic Link) |
|--------------|-----------|---------------------------|
| **Definition** | A direct reference to the file on disk (points to the same inode) | A separate file that points to the original file's path |
| **Inode Sharing** | Shares the same inode as the original file | Has a different inode, pointing to the original file |
| **Works Across Filesystems?** | No | Yes |
| **If Original File is Deleted?** | Hard link still works | Soft link breaks (becomes a "dangling link") |
| **Can Link Directories?** | No | Yes (commonly used for shortcuts) |

### Commands to Create Links
**Create a Hard Link**:  
```bash
ln original_file hard_link
```

**Create a Soft Link**:  
```bash
ln -s original_file soft_link
```

**List File Details (Check Inode Numbers)**:  
```bash
ls -li
```

**Remove Links**:  
```bash
rm hard_link soft_link
```

## ACL vs chmod & ACL vs chown
**ACL (Access Control List)** is an advanced way of managing file permissions beyond traditional **chmod** and **chown**.

### ACL vs chmod

| Feature  | ACL | chmod |
|----------|-----|-------|
| **Fine-Grained Control?** | Yes (allows permissions per user/group) | No (only owner, group, others) |
| **Can Set Different Permissions for Multiple Users?** | Yes | No |
| **Applies to Directories?** | Yes | Yes |

### Example Commands
**Set ACL (Give `read` and `write` permissions to user `sushant` on `file.txt`)**  
```bash
setfacl -m u:sushant:rw file.txt
```

**View ACL Permissions**  
```bash
getfacl file.txt
```

**Remove ACL Permissions**  
```bash
setfacl -x u:sushant file.txt
```


### ACL vs chown

| Feature  | ACL | chown |
|----------|-----|-------|
| **Controls Ownership?** |  No |  Yes |
| **Sets Permissions for Multiple Users?** |  Yes |  No (only one owner/group) |

### Example chown Commands
**Change File Ownership**:  
```bash
chown user:group file.txt
```

**Give Ownership to `sushant` for `folder/`**  
```bash
chown -R sushant:sushant folder/
```



## Most Widely Used kill Commands
In Linux, the **kill** command is used to terminate processes. Each process has a **PID (Process ID)** that we use to kill it.

### Common kill Signals & Their Usage
| Signal | Number | Description |
|--------|--------|-------------|
| `SIGTERM` | `15` | Gracefully stops a process |
| `SIGKILL` | `9` | Forces a process to terminate immediately |
| `SIGHUP` | `1` | Restarts a process |
| `SIGSTOP` | `19` | Pauses a process |
| `SIGCONT` | `18` | Resumes a paused process |


### Common kill Commands
**Find Process ID (PID) of a program**  
```bash
ps aux | grep program_name
```

**Gracefully terminate a process**  
```bash
kill PID
```

**Forcefully kill a process**  
```bash
kill -9 PID
```

**Kill all processes by name**  
```bash
pkill process_name
```

**Kill all processes owned by a user**  
```bash
pkill -u username
```

**Kill a process running on a specific port**  
```bash
fuser -k 8080/tcp
```

**Kill all processes at once (Dangerous! Be Careful!)**  
```bash
kill -9 -1
```

**When to use?**  
- Use `kill -15` to **gracefully terminate** a process.  
- Use `kill -9` only when a process **does not stop normally**.  
- Use `pkill` or `killall` when dealing with **multiple processes**.  


## Apache Web Server 
Apache HTTP Server (commonly known as **Apache**) is a **widely used, open-source web server** that powers millions of websites. It is known for its **flexibility, security, and extensive module support**.

### When to Use Apache?
- **Web Server** – Serves dynamic and static content efficiently.  
- **Reverse Proxy** – Routes requests to backend services or applications.  
- **Load Balancing** – Distributes traffic across multiple backend servers.  
- **Customizable via Modules** – Supports modules like `mod_rewrite`, `mod_ssl`, and `mod_proxy`.  
- **Virtual Hosting** – Hosts multiple websites on a single server.  


### How to Install and Use Apache?
**Install Apache on Linux (CentOS / RHEL)**
```bash
sudo yum install httpd -y
```

**Start and Enable Apache**
```bash
sudo systemctl start httpd
sudo systemctl enable httpd
```

**Check Apache Status**
```bash
sudo systemctl status httpd
```

**Configure Apache (Main Config File)**
```bash
nano /etc/httpd/conf/httpd.conf
```

**Restart Apache After Changes**
```bash
sudo systemctl restart httpd
```


### Apache Configuration File Location 
The default location for Apache configuration files on CentOS/RHEL is:
```bash
/etc/httpd/conf/httpd.conf
```

Other important locations:  
- `/etc/httpd/conf.d/` → Stores additional configuration files.  
- `/var/www/html/` → Default document root for websites.  
- `/var/log/httpd/` → Stores Apache logs (access & error logs).  



## nginx 
Nginx is a **high-performance web server, reverse proxy, and load balancer**. It is widely used due to its **efficiency, scalability, and ability to handle high traffic loads**.

### When to Use Nginx?  
- **Web Server** – Serves static files (HTML, CSS, JS, images, etc.) efficiently.  
- **Reverse Proxy** – Routes client requests to backend servers like Apache, Node.js, etc.  
- **Load Balancer** – Distributes traffic across multiple servers to improve performance.  
- **Caching** – Speeds up content delivery by caching responses.  


### How to Install and Use Nginx?
**Install Nginx on Linux (CentOS / RHEL)**
```bash
sudo yum install nginx -y
```

**Start and Enable Nginx**
```bash
sudo systemctl start nginx
sudo systemctl enable nginx
```

**Check Nginx Status**
```bash
sudo systemctl status nginx
```

**Configure Nginx (Main Config File)**
```bash
nano /etc/nginx/nginx.conf
```

**Restart Nginx after changes**
```bash
sudo systemctl restart nginx
```


### Nginx Configuration File Location  
The default location for Nginx configuration files on CentOS/RHEL is:
```bash
/etc/yum.repos.d/nginx.repo
```

Other important locations:
- `/etc/nginx/nginx.conf` → Main configuration file  
- `/etc/nginx/sites-available/` → Stores individual site configurations  
- `/var/www/html/` → Default document root for websites  


### Apache Web Server vs Nginx Web Server
| Feature | Apache | Nginx |
|---------|--------|-------|
| **Performance** | Slower with high concurrency | Faster, handles thousands of connections efficiently |
| **Architecture** | Process-based (each request creates a new process) | Event-driven (single thread handles multiple connections) |
| **Static Content Handling** | Good | Excellent (faster than Apache) |
| **Dynamic Content Handling (PHP, Python, etc.)** | Supports **mod_php** (better for PHP) | Needs external processors like **FastCGI** |
| **Reverse Proxy Support** | Limited | Strong support for reverse proxying |
| **Configuration** | `.htaccess` allows per-directory configuration | Centralized configuration in `nginx.conf` |
| **Load Balancing** | Requires extra modules | Built-in load balancing |
| **Flexibility** | More customizable due to modules | More efficient for high-traffic sites |

**When to Use Which?**  
- Use **Apache** when hosting PHP-based applications like WordPress.  
- Use **Nginx** for high-traffic sites, as a reverse proxy, or for performance-critical applications.  


## SAMBA Server 
Samba is an **open-source software** that allows **file and print sharing** between Linux and Windows systems. It enables Linux to act as a **Windows-compatible file server**.

### Protocols Used by Samba  
- **SMB (Server Message Block)** – Allows file sharing between Linux and Windows.  
- **CIFS (Common Internet File System)** – A version of SMB used for **network file access**.  


## Handwritten notes

[Link](file:///Users/im_sushant/Developer/Notes/Linux/LINUX%20Notes.pdf)