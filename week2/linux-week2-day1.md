## Shell and Shell Scripting Basics

### What is a Shell?
- A shell is a command-line interpreter that allows users to interact with the operating system.
- It takes user commands and executes them.
- Examples of popular shells:
  - **Bash** (Bourne Again Shell) – Most commonly used in Linux.
  - **Zsh** (Z Shell) – A more advanced version of Bash.
  - **Fish** (Friendly Interactive Shell) – Focuses on ease of use.

---

### What is Shell Scripting?
- Shell scripting is writing a sequence of shell commands in a file and executing them as a script.
- It automates repetitive tasks like backups, monitoring, and software installation.

#### ✅ Advantages of Shell Scripting:
- **Automation** – Reduces manual work.
- **Batch Processing** – Execute multiple commands in a sequence.
- **System Administration** – Manage processes, files, and users.
- **Custom Tools** – Create utilities to perform specific tasks.

---

## Basics of Shell Scripting

### Writing a Shell Script
```bash
# Create a file
vi myscript.sh

# Add the shebang (#!) to specify the interpreter
#!/bin/bash
echo "Hello, Shell Scripting!"

# Make it executable
chmod +x myscript.sh

# Run the script
./myscript.sh
```

---

## Variables in Shell Scripting

### Defining Variables:
```bash
name="Pratik"
age=25
```

### Accessing Variables:
```bash
echo "Name: $name, Age: $age"
```

### Reading User Input:
```bash
read -p "Enter your city: " city
echo "You live in $city."
```

---

## Conditional Statements (If-Else)

### ✅ Syntax:
```bash
if [ condition ]; then
   # Code if condition is true
elif [ another_condition ]; then
   # Code if another_condition is true
else
   # Code if none of the conditions are true
fi
```

### ✅ Example: Check if a number is positive, negative, or zero
```bash
#!/bin/bash

read -p "Enter a number: " num

if [ "$num" -gt 0 ]; then
    echo "Positive"
elif [ "$num" -lt 0 ]; then
    echo "Negative"
else
    echo "Zero"
fi
```

---

## Loops in Shell Scripting

### ✅ For Loop:
```bash
for i in {1..5}; do
    echo "Number: $i"
done
```

### ✅ While Loop:
```bash
i=1
while [ "$i" -le 5 ]; do
    echo "Count: $i"
    ((i++))
done
```

### ✅ Until Loop (Runs until the condition becomes true):
```bash
i=1
until [ "$i" -gt 5 ]; do
    echo "Until Count: $i"
    ((i++))
done
```

---

## 📦 tar Command (Archiving & Compression)

### What is tar?
- `tar` (Tape Archive) is used to combine multiple files into a single archive file.
- It does not compress by default but can be combined with gzip or bzip2 for compression.

### Creating a Tar Archive (.tar)
```bash
tar -cvf archive.tar file1 file2 folder/
```
- `-c` → Create a new archive.
- `-v` → Show progress (verbose).
- `-f` → Specify the archive filename.

### Extracting a Tar Archive
```bash
tar -xvf archive.tar
```
- `-x` → Extract files from the archive.
- `-v` → Show progress.
- `-f` → Specify the archive file.

✅ Extract to a specific folder:
```bash
tar -xvf archive.tar -C /path/to/destination/
```

---

### Creating a Compressed Archive (.tar.gz or .tgz)
```bash
tar -czvf archive.tar.gz file1 file2 folder/
```
- `-z` → Compress using gzip.

✅ Extracting .tar.gz files:
```bash
tar -xzvf archive.tar.gz
```

### Creating a Highly Compressed Archive (.tar.bz2)
```bash
tar -cjvf archive.tar.bz2 file1 file2 folder/
```
- `-j` → Compress using bzip2 (better compression but slower).

✅ Extracting .tar.bz2 files:
```bash
tar -xjvf archive.tar.bz2
```

### Viewing Contents of a Tar Archive
```bash
tar -tvf archive.tar
```
- `-t` → List the files inside the archive without extracting.

### Adding Files to an Existing Tar Archive
```bash
tar -rvf archive.tar newfile.txt
```
🚨 **Note:** This does not work for compressed archives (.tar.gz).

### Deleting a File from a Tar Archive
```bash
tar --delete -f archive.tar file1.txt
```
🚨 **Note:** You cannot delete from compressed archives (.tar.gz).

### Extracting a Single File from a Tar Archive
```bash
tar -xvf archive.tar file1.txt
```
✅ Extract Multiple Files:
```bash
tar -xvf archive.tar file1.txt file2.txt
```

---

## 🔍 Summary of tar Options
| Action | Command |
|--------|---------|
| Create .tar | `tar -cvf archive.tar files` |
| Create .tar.gz | `tar -czvf archive.tar.gz files` |
| Create .tar.bz2 | `tar -cjvf archive.tar.bz2 files` |
| Extract .tar | `tar -xvf archive.tar` |
| Extract .tar.gz | `tar -xzvf archive.tar.gz` |
| List contents | `tar -tvf archive.tar` |
| Add to archive | `tar -rvf archive.tar newfile.txt` |
| Delete from archive | `tar --delete -f archive.tar file1.txt` |

---

## HackerRank Problems

1. **Problem 1:** [Let's Echo](https://www.hackerrank.com/challenges/bash-tutorials-lets-echo/problem?isFullScreen=true)
    ![image](https://github.com/user-attachments/assets/aebba1be-4147-4b21-a741-2f0078529526)

2. **Problem 2:** [Looping and Skipping](https://www.hackerrank.com/challenges/bash-tutorials---looping-and-skipping/problem?isFullScreen=true)
    ![image](https://github.com/user-attachments/assets/6246cda9-ddef-4744-9a55-cf375d45be26)

3. **Problem 3:** [A Personalized Echo](https://www.hackerrank.com/challenges/bash-tutorials---a-personalized-echo/problem?isFullScreen=true)
    ![image](https://github.com/user-attachments/assets/343810b5-c68d-4ffb-b1c0-685b4e8790fd)

4. **Problem 4:** [Looping with Numbers](https://www.hackerrank.com/challenges/bash-tutorials---looping-with-numbers/problem?isFullScreen=true)
    ![image](https://github.com/user-attachments/assets/d3a2c505-1e09-43aa-92b5-c75ddaaae914)

5. **Problem 5:** [The World of Numbers](https://www.hackerrank.com/challenges/bash-tutorials---the-world-of-numbers/problem?isFullScreen=true)
    ![image](https://github.com/user-attachments/assets/da5ac62f-e440-4bbd-805b-4eccce526d4f)

6. **Problem 6:** [Comparing Numbers](https://www.hackerrank.com/challenges/bash-tutorials---comparing-numbers/problem?isFullScreen=true)
    ![image](https://github.com/user-attachments/assets/eb3ab88c-a7c6-4ce3-9fc6-0f8fef26a67b)

7. **Problem 7:** [Getting Started with Conditionals](https://www.hackerrank.com/challenges/bash-tutorials---getting-started-with-conditionals/problem?isFullScreen=true)
    ![image](https://github.com/user-attachments/assets/0452270e-96bf-4562-a3c7-83b364527a95)

8. **Problem 8:** [Compute the Average](https://www.hackerrank.com/challenges/bash-tutorials---compute-the-average/problem?isFullScreen=true)
    ![image](https://github.com/user-attachments/assets/b87515a2-2ce3-48fd-88fb-d1733349412f)
