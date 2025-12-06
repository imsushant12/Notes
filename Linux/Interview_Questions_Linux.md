- **Question 1: What is root in Linux?**  
  - **Answer**:  The `root` is the superuser account in Linux with unlimited privileges, allowing full control over the system. It can manage users, files, and processes. Using `root` should be limited for security reasons, and `sudo` is preferred for administrative tasks.

- **Question 2: What is inode and how to find it for a file?**  
  - **Answer**: An `inode` is a data structure in Linux that stores metadata about a file, such as size, ownership, and permissions, but not the file name or content.  
    - **Code:**  
      ```bash
      ls -i <file_name>
      ```

- **Question 3: Which commands are used to find files on a Linux server?**  
  - **Answer**:  
    - `find`: Searches files in a directory hierarchy.  
      ```bash
      find /path -name <file_name>
      ```  
    - `locate`: Uses a pre-built database for fast file search.  
      ```bash
      locate <file_name>
      ```  
    - `grep`: Searches for specific patterns inside files.  
      ```bash
      grep "text" <file_name>
      ```

- **Question 4: How to install anything on a Linux server?**  
  - **Answer**: Use the package manager:  
    - For Ubuntu/Debian:  
      ```bash
      sudo apt update && sudo apt install <package_name>
      ```  
    - For Red Hat/CentOS:  
      ```bash
      sudo yum install <package_name>
      ```

- **Question 5: How to combine 2 commands and how to use `|` command?**  
  - **Answer**:  
    - Combine commands:  
      - `&&`: Run the next command only if the first succeeds.  
        ```bash
        mkdir test_dir && cd test_dir
        ```  
      - `||`: Run the next command only if the first fails.  
        ```bash
        mkdir test_dir || echo "Failed to create directory."
        ```  
    - Use `|` (pipe) to pass output from one command to another:  
      ```bash
      ls | grep <pattern>
      ```

- **Question 6: How to permanently delete a file so it cannot be recovered?**  
  - **Answer**: Use `shred` to overwrite the file with random data before deletion:  
    - **Code:**  
      ```bash
      shred -u <file_name>
      ```

- **Question 7: How to check system architecture information?**  
  - **Answer**:  
    Use:  
    - **Code:**  
      ```bash
      uname -m
      ```  
    For detailed information:  
    - **Code:**  
      ```bash
      lscpu
      ```

- **Question 8: How to check the type of a file?**  
  - **Answer**: Use the `file` command:  
    - **Code:**  
      ```bash
      file <file_name>
      ```

- **Question 9: What are the different ways to access a Linux server remotely?**  
  - **Answer**:  
    - **SSH (Secure Shell):** Most common and secure.  
    - **Telnet:** Rarely used due to lack of encryption.  
    - **RDP (Remote Desktop Protocol):** For GUI-based access.  
    - **VNC:** For remote desktop sharing.

- **Question 10: How to redirect an error of a command into a file?**  
  - **Answer**: Use `2>` to redirect errors:  
    - **Code:**  
      ```bash
      command 2> error.log
      ```

- **Question 11: How to automate any script or task in Linux?**  
  - **Answer**: Use `cron` jobs for automation. Add tasks to the crontab:  
    - **Code:**  
      ```bash
      crontab -e
      ```

- **Question 12: What is the meaning of this cron job `* * * * *`?**  
  - **Answer**: It means the task will run **every minute**.

- **Question 13: If your cron job did not work, how would you check it?**  
  - **Answer**:  
    - Check the cron logs:  
      - **Code:**  
        ```bash
        grep CRON /var/log/syslog
        ```  
    - Ensure the cron service is running:  
      - **Code:**  
        ```bash
        sudo systemctl status cron
        ```

- **Question 14: What is a daemon service? Examples?**  
  - **Answer**: A daemon is a background process that runs continuously to perform tasks or handle requests. Examples include:  
    - `sshd` (SSH daemon)  
    - `httpd` (Web server daemon)

- **Question 15: How to check if a server is accessible or not?**  
  - **Answer**: Use the `ping` command:  
    - **Code:**  
      ```bash
      ping <server_ip_or_hostname>
      ```

- **Question 16: How to check network interfaces in Linux?**  
  - **Answer**:  
    Use:  
    - **Code:**  
      ```bash
      ifconfig
      ```  
    or:  
    - **Code:**  
      ```bash
      ip a
      ```

- **Question 17: What is the difference between Telnet and SSH?**  
  - **Answer**:  
    - **Telnet:** Unencrypted, insecure, and rarely used.  
    - **SSH:** Encrypted and secure for remote access.

- **Question 18: Which service should be running on the server to allow you to connect remotely?**  
  - **Answer**: The **SSH (Secure Shell)** service must be running. Check it using:  
    - **Code:**  
      ```bash
      sudo systemctl status ssh
      ```

- **Question 19: Why is SSH called a secure shell?**  
  - **Answer**: SSH encrypts data during transmission, preventing eavesdropping and man-in-the-middle attacks.

- **Question 20: What is the default port of SSH?**  
  - **Answer**: The default port is **22**.

- **Question 21: If you have to send a large file remotely, what would be the first thing you would do?**  
  - **Answer**: Compress the file using `tar` or `gzip`:  
    - **Code:**  
      ```bash
      tar -czvf file.tar.gz <file_name>
      ```  
    Then transfer it using `scp` or `rsync`.

- **Question 22: What is the difference between tar, gzip, and gunzip?**  
  - **Answer**:  
    - **tar:** Combines multiple files into a single archive.  
    - **gzip:** Compresses files.  
    - **gunzip:** Decompresses `.gz` files.


- **Question 23: What is swap space in LiNUX?**
  - **Answer**: 
- **Question 24: What is SCP command and what does scp command uses?**
  - **Answer**: 
- **Question 25: What is the difference between update and upgrade command?**
  - **Answer**:
- **Question 26: What are some of the most used protocols in LINUX and what rae their ports?**
  - **Answer**:
- **Question 27: How to check if a package is installed on the system or not?**
  - **Answer**:
- **Question 28: Which file contains the list of group names?**
  - **Answer**: `/etc/group/`
- **Question 29: ?**
  - **Answer**:
- **Question 30: How to check if a package is installed on the system or not?**
  - **Answer**:
- **Question: How can you find the exit status of the previous command?**
  - **Answer**: `$?`
- **Question: How can we execute multiple commands together?**
  - **Answer**: Using semicolon (`;`)
- **Question: What are the valid values of exit status ?**
  - **Answer**: It is 0 to 255 where 0 means successful.
- **Question: What is the default directory of logs?**
  - **Answer**: `/var/log/`
- **Question: Does ping command uses any port?**
  - **Answer**: No
- **Question: What is the difference between locate and find? Which is faster and why?**
  - **Answer**:
- **Question: What is xargs?**
  - **Answer**:
- **Question: How can you calculate the total number of files and directories in a directory?**
  - **Answer**:
- **Question: How can you read the 25-30th line from a file?**
  - **Answer**:  
- **Question: What is the use of `at` command? Which service does `at` command uses?**
  - **Answer**:
- **Question: What is ACL and what are its advantages?**
  - **Answer**: 
- **Question: What are links in LINUX ans its types and differences?**
  - **Answer**:
- **Question: How can you check all the environment variables?**
  - **Answer**: `env` or `printenv`
- **Question: ?**
  - **Answer**:
- **Question: How can you set environment variables in LINUX?**
  - **Answer**:
- **Question: How to see all the process IDs of a process?**
  - **Answer**:
- **Question: What is nice value of a process and what is its range?**
  - **Answer**:
- **Question: How can you make a process run faster than the default rate?**
  - **Answer**:
- **Question: How can you check the %memory and %cpu of a process?**
  - **Answer**:
- **Question: How can you run a script in background even if the terminal closes?**
  - **Answer**:
- **Question: How can you see all the active jobs?**
  - **Answer**:
- **Question: How can you display information about kernel-related message, system-startup message stored in kernel etc?**
  - **Answer**:
- **Question: How would you display all the files in a directory which starts with a given letter or letters? Example that starts with "b" or "d".**
  - **Answer**:
- **Question: What is a VM and what is a hypervisor?**
  - **Answer**:
- **Question: What are the types of hypervisor?**
  - **Answer**:
- **Question: ?**
  - **Answer**:
- **Question: ?**
  - **Answer**:
- **Question: ?**
  - **Answer**:
- **Question: ?**
  - **Answer**: