# Linux Commands and Shell Scripting Overview

## 1. Basic File and Directory Management

### Create and Remove Files or Directories:
- `rmdir -p directory_name` – Removes a directory and its parent directories if they are empty.
- `rm -rf file_name` – Forcefully removes a file or directory, even if it’s not empty.

### View and Create Files:
- `vi file_name` – Opens the file in the vi editor for editing.
- `cat file_name` – Displays the content of the file in the terminal.
- `echo "text" > file_name` – Inserts text into a file.

  ![image](https://github.com/user-attachments/assets/9ea208af-6789-4636-add9-f942c7857cd2)


### Get Help:
- `man command_name` – Displays the manual page for a command (e.g., `man rmdir`).
![image](https://github.com/user-attachments/assets/1f142eca-4f68-4f30-a1f3-ba834efb600e)

## 2. System Information

### Display System Information:
- `uname -a` – Displays detailed system information.
- `uname -r` – Displays the kernel release version.
- `uname -s` – Shows the kernel name.
- `uname -v` – Displays the kernel version.
- `uname -m` – Displays machine architecture.
- `uname -p` – Shows the processor type.
- `uname -i` – Displays the hardware platform.
- `uname -o` – Shows the operating system.

![image](https://github.com/user-attachments/assets/c18c278a-449e-413a-abd5-6ccd26a1d1d2)

## 3. Process Management

### List Running Processes:
- `ps aux` – Lists all currently running processes.

![image](https://github.com/user-attachments/assets/9db076c2-ca23-418a-8355-fc003edf377b)

### Kill a Process:
- `kill -9 process_id` – Forcefully kills a process by its ID.

### Identify the User:
- `whoami` – Displays the current user working on the system.

## 4. Text Processing and File Management

### Sort Text in Files:
- `sort file_name` – Sorts text in ascending order.
- `sort -r file_name` – Sorts text in descending order.

![image](https://github.com/user-attachments/assets/f90dd487-2bfa-47c5-bd74-501c3d2cef31)

### Count Lines, Words, and Characters in a File:
- `wc -l file_name` – Counts the number of lines in a file.
- `wc -w file_name` – Counts the number of words in a file.
- `wc -c file_name` – Counts the number of characters in a file.
- `wc *` – Counts the number of files in the directory.

![image](https://github.com/user-attachments/assets/568cabdf-1d41-4cc8-b367-c122965714e8)

### Search and Filter Content:
- `history | grep text` – Searches for a specific text in the command history.
- `awk '{print $1}' data.txt` – Prints the first column of a file.
- `awk '/pattern/' data.txt` – Filters lines based on a pattern.
![image](https://github.com/user-attachments/assets/5ce3ddb4-616a-4bd6-b36c-763d198cd47f)

## 5. Working with Dates and Time

### Display Current Time:
- `date +%H` – Displays the current hour.
  
###	Conditional statements based on time:

![image](https://github.com/user-attachments/assets/2c787be4-11bd-4cdd-834f-7324106cbc9e)

### Set the Timezone:
- `sudo timedatectl set-timezone Asia/Kolkata` – Sets the system's timezone to Asia/Kolkata.

![image](https://github.com/user-attachments/assets/a5773994-d2ef-4e0c-b027-92676f2423e9)

## 6. Installing Packages and Using Additional Tools

### Install Packages:
- `sudo apt install ncal` – Installs the ncal package for displaying calendars.

### Use the ncal Command:
- `ncal` – Displays the current month's calendar.
- `cal 2025` – Displays the calendar for the year 2025.

### Disk Usage:
- `ncdu .` – Displays disk usage of files in the current directory.

  ![image](https://github.com/user-attachments/assets/27059689-f760-4e2f-8055-179e011e384d)



## 7. Shell Scripting and Variables

### Create a Shell Script:
- `vi script.sh` – Opens the shell script for editing.
- `chmod +x script.sh` – Makes the script executable.
- `./script.sh` – Executes the script.
  
![image](https://github.com/user-attachments/assets/5f68daa6-1862-42d2-8e81-5e2f07176651)


![image](https://github.com/user-attachments/assets/804771d9-0acc-4c45-9603-455236a103c4)

## 8. Loops and Conditionals

![image](https://github.com/user-attachments/assets/15548b20-3f41-46c6-80eb-66ecf6ccd7ea)

### While Loop and For Loop

## 9. File Compression and Archiving (tar)

### Create a TAR Archive:
- `tar -cvf archive.tar file1.txt file2.txt`

### Extract Files from a TAR Archive:
- `tar -xvf archive.tar`

### List the Contents of a TAR Archive:
- `tar -tvf archive.tar`

### Compress Files with gzip:
- `tar -cvf archive.tar.gz *` – Creates a gzipped tar archive.
- `tar -xzvf archive.tar.gz` – Extracts a gzipped tar archive.

### Adding Files to an Existing Tar Archive:
- `tar -rvf archive.tar newfile.txt`

### Deleting a File from a Tar Archive:
- `tar --delete -f archive.tar file1.txt`

### Summary of Commonly Used tar Commands:
| Command | Description |
|---------|-------------|
| `tar -cvf archive.tar file1 file2` | Create a tar archive (archive.tar) from file1 and file2. |
| `tar -xvf archive.tar` | Extract the contents of archive.tar. |
| `tar -tvf archive.tar` | List the contents of archive.tar. |
| `tar -czvf archive.tar.gz *` | Create a gzipped tar archive (archive.tar.gz). |
| `tar -xzvf archive.tar.gz` | Extract a gzipped tar archive (archive.tar.gz). |
| `tar -cvf archive.tar --exclude='*.log'` | Create a tar archive excluding .log files. |
| `tar -czf archive.tar.gz folder/` | Create a gzipped tar archive of a folder. |
| `tar -tf archive.tar` | List the contents of a tar archive without extracting. |

### Key Options:
- `-c`: Create an archive.
- `-x`: Extract an archive.
- `-v`: Verbose (shows the files being processed).
- `-f`: Specify the archive file name.
- `-t`: List the contents of the archive.
- `-z`: Compress with gzip.
- `--exclude`: Exclude files from being archived.
![image](https://github.com/user-attachments/assets/6acfd45d-ab63-4e7e-8f34-f280c207d304)
![image](https://github.com/user-attachments/assets/d7592bd6-8b38-4789-894a-00338a1871fc)

## 10. File Searching

### Find Files by Name:
- `find -name "*.txt"` – Finds all .txt files in the current directory and subdirectories.

### Find Directories:
- `find . -type d` – Finds all directories starting from the current directory.

## Difference Between Find and Plocate
- `find` is slower but offers more flexibility and real-time accuracy.
- `plocate` is faster, especially for large directories, and uses an efficient indexed search.

## Conclusion
This document provides a concise overview of basic Linux commands, file management, system information retrieval, process management, text processing, file compression, shell scripting, and more.

## Hacker Rank Problems
1. [Problem 1](https://www.hackerrank.com/challenges/bash-tutorials-lets-echo/problem?isFullScreen=true)
  ![image](https://github.com/user-attachments/assets/e5ba93aa-74ed-427e-aea9-83f0d302b25b)

2. [Problem 2](https://www.hackerrank.com/challenges/bash-tutorials---looping-and-skipping/problem?isFullScreen=true)
    ![image](https://github.com/user-attachments/assets/26b4e95b-6f66-4501-90b3-51a2e6dc57c6)

3. [Problem 3](https://www.hackerrank.com/challenges/bash-tutorials---a-personalized-echo/problem?isFullScreen=true)
    ![image](https://github.com/user-attachments/assets/0eec20e7-212c-4da9-a768-49c2324f4edd)

4. [Problem 4](https://www.hackerrank.com/challenges/bash-tutorials---looping-with-numbers/problem?isFullScreen=true)
    ![image](https://github.com/user-attachments/assets/fbda114e-7a25-4912-89ca-10bacb6a5c15)

5. [Problem 5](https://www.hackerrank.com/challenges/bash-tutorials---the-world-of-numbers/problem?isFullScreen=true)
  ![image](https://github.com/user-attachments/assets/b4c2e34d-4c59-40aa-87ad-0d03e1713fb1)

6. [Problem 6](https://www.hackerrank.com/challenges/bash-tutorials---comparing-numbers/problem?isFullScreen=true)
    ![image](https://github.com/user-attachments/assets/137cf2af-7535-4c0c-89d6-c343afafbe2a)

7. [Problem 7](https://www.hackerrank.com/challenges/bash-tutorials---getting-started-with-conditionals/problem?isFullScreen=true)
    ![image](https://github.com/user-attachments/assets/d639d584-ac66-4b2b-ad4c-20ca74cd34fc)

8. [Problem 8](https://www.hackerrank.com/challenges/bash-tutorials---compute-the-average/problem?isFullScreen=true)
    ![image](https://github.com/user-attachments/assets/672aef14-ee00-4640-a402-5ecb4cbb2ee1)
