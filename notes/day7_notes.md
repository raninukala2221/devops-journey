# Day 7: Linux File Links, Compression, and Backups

## 1. What is a Linux Inode?

To understand links, you must understand how Linux saves files. Every file has two parts:

1. **The Content:** The actual data text saved on the hard drive.
2. **The Metadata:** The file size, owner, and permissions. Linux saves this information in a hidden slot called an **Inode (Index Number)**.

Every file name is just a label that points to an Inode number.

### System Check Commands

* `ls -i` : Shows the hidden Inode tracking number of a file.
* `ls -l` : Shows the full details of a file (size, owner, permissions).
* `ls -li` : Shows both the Inode number and the full details together.

#### Example:

```bash
\$ ls -li sample.txt
123456 -rw-r--r--. 1 rani users 45 Jun 05 13:00 sample.txt
# [Inode] [Perms] [Links] [Owner] [Group] [Size] [Date] [Name]
```

---

## 2. File Links: Soft Links vs. Hard Links

A link is a shortcut to a file. There are two types of links in Linux.

### A. Soft Links (Symbolic Links / Shortcuts)

* **What it is:** A soft link is like a Windows shortcut. It is a tiny file that simply points to the path of another file.

* **Key Rules:**
  * The original file and the soft link have **different Inode numbers**.
  * You can create a soft link across different hard drives or networks.
  * If you delete the original file, the soft link breaks and stops working.
  * A soft link shows the letter **l** at the start of its details line when you type `ls -l`.

#### Syntax:

```bash
ln -s <path_of_original_file> <name_of_shortcut>
```

#### Meaning of the Syntax:
* `ln` : The link tool command.
* `-s` : Tells the system to make a soft link instead of a hard link.
* `<source_file>` : The original file path.
* `<link_file>` : The new shortcut name you want to create.

#### Examples to Practice:

* **Create a shortcut to a folder:**
  ```bash
  ln -s /var/www/html/app /tmp/my_shortcut
  ```
* **Check if the shortcut works:**
  ```bash
  ls -li /tmp/my_shortcut
  ```

---

### B. Hard Links

* **What it is:** A hard link creates a direct copy of the filename label. Both labels point to the exact same Inode on the disk.

* **Key Rules:**
  * The original file and the hard link share the **exact same Inode number**.
  * You cannot create a hard link across different hard drives.
  * If you edit one file, the changes instantly show in the other file.
  * If you delete the original file, your data is **not lost**. The data vanishes only when you delete all hard links to it.

#### Syntax:

```bash
ln <path_of_original_file> <name_of_hard_link>
```

#### Examples to Practice:

* **Protect an important configuration file:**
  ```bash
  ln /etc/nginx/nginx.conf /root/config_backup_link
  ```
* **Verify that they share the same Inode:**
  ```bash
  ls -li /etc/nginx/nginx.conf /root/config_backup_link
  ```
* **Delete a hard link safely:**
  ```bash
  unlink /root/config_backup_link
  ```

---

## 3. File Compression Tools

Compression makes files smaller. Smaller files save space and download faster over the internet.



| Tool Name | File Extension | Speed vs. Size | How to Decompress | Works on Windows? |
| :--- | :--- | :--- | :--- | :--- |
| **gzip** | .gz | Very fast, medium size reduction. | gunzip | No |
| **bzip2** | .bz2 | Slower, makes files very small. | bunzip2 | No |
| **zip** | .zip | Medium speed, medium size reduction. | unzip | Yes (Universal) |

#### Examples to Practice:

* **Compress a log file using gzip:**
  ```bash
  gzip system.log
  # This creates system.log.gz and deletes the original file.
  ```
* **Decompress a gzip file:**
  ```bash
  gunzip system.log.gz
  ```
* **Zip multiple files together using universal zip:**
  ```bash
  zip backup.zip note1.txt note2.txt
  ```

---

## 4. Packing Files with TAR (Tape Archive)

The tools `gzip` and `bzip2` can only compress single files. They cannot compress whole folders. Linux uses the `tar` command to pack a whole folder into a single file before compressing it.

### Key Letter Options

* `-c` : **Create** a new backup file.
* `-x` : **Extract** (unzip) a backup file back into folders.
* `-v` : **Verbose** (shows the progress on the screen while working).
* `-f` : **File** (tells the system you are saving to a file name).
* `-t` : **Test** (shows the list of files inside the backup without unzipping it).
* `-r` : **Read/Append** (adds a forgotten file to an existing backup).
* `-z` : Tells tar to use **gzip** compression automatically (`.tar.gz`).
* `-j` : Tells tar to use **bzip2** compression automatically (`.tar.bz2`).

### Practice Commands

* **Pack a folder without compression:**
  ```bash
  tar -cvf my_backup.tar /home/rani/project/
  ```
* **Add a forgotten file to your backup:**
  ```bash
  tar -rvf my_backup.tar script.py
  ```
* **See what is inside the backup without extracting it:**
  ```bash
  tar -tvf my_backup.tar
  ```
* **Create a high-quality compressed backup (Standard DevOps practice):**
  ```bash
  tar -czvf production.tar.gz file1.txt file2.txt folder1/
  ```
* **Extract a compressed backup folder:**
  ```bash
  tar -xzvf production.tar.gz
  ```
* **Extract only one specific file from a big backup:**
  ```bash
  tar -xzvf production.tar.gz file1.txt
  ```

---

## 5. Day 7 Hands-on Practice Lab

Run these commands inside your CentOS terminal to practice what you learned today:

```bash
# 1. Create a practice folder and go inside
mkdir ~/practice_lab && cd ~/practice_lab

# 2. Create a test file with text
echo "Hello DevOps World" > source.txt

# 3. Create a hard link and a soft link
ln source.txt hard_link.txt
ln -s ~/practice_lab/source.txt soft_link.txt

# 4. Check the Inode numbers
ls -li

# 5. Test what happens when you delete the source file
rm source.txt
cat hard_link.txt   # This works perfectly!
cat soft_link.txt   # This gives an error! (The shortcut is broken)

# 6. Create a zipped backup of your practice folder
cd ~
tar -czvf lab_backup.tar.gz practice_lab/
```
