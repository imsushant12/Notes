## 1. System Monitoring
1.1. `df`  
**Flags:** `-h` (human-readable format), `-Th` (display file system type)  

1.2. `du`  
**Flags:** `-h` (human-readable format)  

1.3. `top`  
**Flags:** None  

1.4. `ps`  
**Flags:** `-l`, `-e`, `-A`, `-ef`, `-u`, `-G`, `-ejH`, `aux` (detailed process listing)  

1.5. `pgrep`  
**Flags:** None  

1.6. `pidof`  
**Flags:** None  

1.7. `nice`  
**Flags:** `-n` (set priority)  

1.8. `renice`  
**Flags:** `-p` (change process priority)  

1.9. `kill`  
**Flags:** `-9` (forcefully terminate a process), `-l` (list signals)  

1.10. `pkill`  
**Flags:** None  

1.11. `jobs`  
**Flags:** None  

1.12. `bg`  
**Flags:** None  

1.13. `fg`  
**Flags:** None  

1.14. `dmesg`  
**Flags:** `-HTx` (formatted output), `-w` (follow new messages), `-c` (clear log), `-l` (show level-specific logs)  

1.15. `uptime`  
**Flags:** None  

1.16. `free`  
**Flags:** `-h` (human-readable format), `-th` (total and human-readable format)  

1.17. `lsblk`  
**Flags:** `-f` (display file system info)  

1.18. `arch`  
**Flags:** None  

1.19. `uname`  
**Flags:** `-a` (display all system information)  


## 2. File and Directory Management
2.1. `ls`  
**Flags:** `-lt` (sorted by modification time), `-ltr` (reverse sorting), `-lh` (human-readable size), `-l` (detailed view), `-a` (show hidden files), `-la` (detailed + hidden files), `-li` (inode details)  

2.2. `ll`  
**Flags:** None  

2.3. `pwd`  
**Flags:** None  

2.4. `whoami`  
**Flags:** None  

2.5. `mkdir`  
**Flags:** None  

2.6. `rmdir`  
**Flags:** None  

2.7. `rm`  
**Flags:** `-rf` (forcefully remove directories and files)  

2.8. `mv`  
**Flags:** None  

2.9. `cp`  
**Flags:** None  

2.10. `touch`  
**Flags:** None  

2.11. `find`  
**Flags:** `-name` (search by name), `-size`, `-type`, `-iname`, `-user`, `-inum`, `-links`, `-perm`, `-newer`, `-empty`, `-mtime` (search by modified time)  

2.12. `locate`  
**Flags:** None  

2.13. `updatedb`  
**Flags:** None  

## 3. Text Processing and Filtering
3.1. `cat`  
**Flags:** None  

3.2. `more`  
**Flags:** None  

3.3. `less`  
**Flags:** None  

3.4. `head`  
**Flags:** `-n` (specify number of lines)  

3.5. `tail`  
**Flags:** `-n` (specify number of lines)  

3.6. `sort`  
**Flags:** `-r` (reverse sorting)  

3.7. `uniq`  
**Flags:** None  

3.8. `shuf`  
**Flags:** None  

3.9. `split`  
**Flags:** `-l` (split by lines)  

3.10. `grep`  
**Flags:** `-i` (case-insensitive), `-v` (invert match), `-c` (count matches), `-w` (whole word match), `-n` (show line number), `-h` (hide filename), `-e` (multiple patterns), `-l` (list filenames with matches), `-f` (read patterns from file), `-R` (recursive search), `-q` (quiet mode), `^keyword`, `keyword$` (match beginning/end of line)  

3.11. `egrep`  
**Flags:** None  

3.12. `fgrep`  
**Flags:** None  

3.13. `pdfgrep`  
**Flags:** None  

3.14. `wc`  
**Flags:** None  

3.15. `cmp`  
**Flags:** None  

3.16. `diff`  
**Flags:** `-u` (unified format)  

3.17. `awk`  
**Flags:** `-F` (define field separator)  

3.18. `cut`  
**Flags:** `-c` (select specific characters)  

3.19. `sed`  
**Flags:** `-n`, `-f`, `-i`, `s/from/to/g` (substitution)  

3.20. `tr`  
**Flags:** `-d` (delete characters), `[:lower:]` (convert to lowercase), `[:upper:]` (convert to uppercase), `[:punct:]` (remove punctuation), `[:digit:]` (remove digits)  

3.21. `xargs`  
**Flags:** None  

## 4. Networking
4.1. `ping`  
**Flags:** `-c` (set number of packets), `-i` (interval), `-s` (packet size)  

4.2. `wget`  
**Flags:** None  

4.3. `curl`  
**Flags:** `-o` (output file), `-I` (fetch headers only), `-X` (HTTP method), `-d` (send data)  

4.4. `scp`  
**Flags:** `-r` (recursive)  

4.5. `rsync`  
**Flags:** `-avz` (archive mode, verbose, compressed)  

4.6. `ftp`  
**Flags:** None  

4.7. `sftp`  
**Flags:** None  

4.8. `netstat`  
**Flags:** `-an` (list all active connections), `-tulnp` (list ports with process details)  

4.9. `ss`  
**Flags:** `-tulnp` (list open ports with process details)  

4.10. `ifconfig`  
**Flags:** None  

4.11. `ip`  
**Flags:** `addr show`, `route show`  

4.12. `hostname`  
**Flags:** None  

4.13. `nslookup`  
**Flags:** None  

4.14. `dig`  
**Flags:** None  

4.15. `traceroute`  
**Flags:** None  

4.16. `telnet`  
**Flags:** None  

4.17. `nmap`  
**Flags:** `-sP` (ping scan), `-sS` (stealth scan), `-O` (OS detection)  

4.18. `arp`  
**Flags:** `-a` (show ARP table)  

4.19. `route`  
**Flags:** `-n` (display routing table)  

## 5. Archiving and Compression
5.1. `tar`  
**Flags:** `-cf` (create archive), `-xf` (extract), `-tvf` (list files), `-z` (gzip), `-j` (bzip2), `-J` (xz)  

5.2. `zip`  
**Flags:** None  

5.3. `unzip`  
**Flags:** None  

5.4. `gzip`  
**Flags:** None  

5.5. `gunzip`  
**Flags:** None  

5.6. `bzip2`  
**Flags:** None  

5.7. `bunzip2`  
**Flags:** None  

5.8. `xz`  
**Flags:** None  

5.9. `unxz`  
**Flags:** None  

5.10. `7z`  
**Flags:** None  

## 6. User Management
6.1. `who`  
**Flags:** None  

6.2. `w`  
**Flags:** None  

6.3. `whoami`  
**Flags:** None  

6.4. `id`  
**Flags:** None  

6.5. `groups`  
**Flags:** None  

6.6. `useradd`  
**Flags:** `-m` (create home directory)  

6.7. `usermod`  
**Flags:** `-aG` (add user to a group)  

6.8. `passwd`  
**Flags:** None  

6.9. `chage`  
**Flags:** `-l` (list password aging info)  

6.10. `groupadd`  
**Flags:** None  

6.11. `groupdel`  
**Flags:** None  

6.12. `gpasswd`  
**Flags:** None  

6.13. `su`  
**Flags:** None  

6.14. `sudo`  
**Flags:** None  

6.15. `visudo`  
**Flags:** None  

6.16. `deluser`  
**Flags:** None  

6.17. `delgroup`  
**Flags:** None  

## 7. Job Scheduling and Process Management
7.1. `crontab`  
**Flags:** `-e` (edit), `-l` (list), `-r` (remove)  

7.2. `at`  
**Flags:** `-l` (list), `-r` (remove)  

7.3. `batch`  
**Flags:** None  

7.4. `nohup`  
**Flags:** None  

7.5. `disown`  
**Flags:** None  

7.6. `bg`  
**Flags:** None  

7.7. `fg`  
**Flags:** None  

## 8. File Permissions and Ownership
8.1. `chmod`  
**Flags:** `-R` (recursive), `+x` (add execute permission), `u/g/o` (user/group/others), `777` (full permission)  

8.2. `chown`  
**Flags:** `-R` (recursive)  

8.3. `chgrp`  
**Flags:** `-R` (recursive)  

8.4. `umask`  
**Flags:** None  

8.5. `lsattr`  
**Flags:** None  

8.6. `chattr`  
**Flags:** `+i` (immutable), `-i` (remove immutable)  

## 9. Disk and Filesystem Management
9.1. `df`  
**Flags:** `-h` (human-readable)  

9.2. `du`  
**Flags:** `-sh` (summarize, human-readable)  

9.3. `mount`  
**Flags:** `-t` (specify filesystem type)  

9.4. `umount`  
**Flags:** None  

9.5. `fsck`  
**Flags:** None  

9.6. `tune2fs`  
**Flags:** None  

9.7. `blkid`  
**Flags:** None  

9.8. `mkfs`  
**Flags:** `-t` (filesystem type)  

9.9. `e2fsck`  
**Flags:** None  

9.10. `resize2fs`  
**Flags:** None  

9.11. `xfs_check`  
**Flags:** None  

9.12. `xfs_repair`  
**Flags:** None  

9.13. `lsof`  
**Flags:** `-i` (network connections), `+D` (directory files)  

9.14. `fuser`  
**Flags:** `-k` (kill processes using a file)  

## 10. System Administration
10.1. `uname`  
**Flags:** `-a` (all details)  

10.2. `uptime`  
**Flags:** None  

10.3. `dmesg`  
**Flags:** `-T` (timestamp)  

10.4. `vmstat`  
**Flags:** None  

10.5. `iostat`  
**Flags:** None  

10.6. `mpstat`  
**Flags:** None  

10.7. `sar`  
**Flags:** None  

10.8. `free`  
**Flags:** `-m` (show memory in MB)  

10.9. `top`  
**Flags:** None  

10.10. `htop`  
**Flags:** None  

10.11. `ps`  
**Flags:** `-ef` (detailed processes)  

10.12. `kill`  
**Flags:** `-9` (force kill)  

10.13. `pkill`  
**Flags:** `-9` (force kill by name)  

10.14. `nice`  
**Flags:** `-n` (set priority)  

10.15. `renice`  
**Flags:** None  

10.16. `iotop`  
**Flags:** None  

10.17. `strace`  
**Flags:** None  

10.18. `time`  
**Flags:** None  


## 11. Miscellaneous Commands
11.1. `alias`  
**Flags:** None  

11.2. `unalias`  
**Flags:** None  

11.3. `history`  
**Flags:** None  

11.4. `clear`  
**Flags:** None  

11.5. `reset`  
**Flags:** None  

11.6. `uptime`  
**Flags:** None  

11.7. `watch`  
**Flags:** None  

11.8. `screen`  
**Flags:** None  

11.9. `tmux`  
**Flags:** None  

11.10. `yes`  
**Flags:** None  