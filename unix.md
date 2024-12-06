### Unix Permissions

#### **Users**  



```bash

# create user
sudo useradd username

# change the password
sudo passwd username

# switch user
su - username

```
- Unix permissions revolve around three user types: **Owner**, **Group**, and **Others**.  
- Permissions include **read (r)**, **write (w)**, and **execute (x)** for each user type.  
- Use `chmod` to modify permissions, `chown` to change file ownership, and `chgrp` to change group ownership.  

#### **Files**  
- Regular files, directories, symbolic links, etc., all have specific permission settings.  
- **`ls -l`** shows detailed permissions in the format: `-rwxr-xr--` (Owner, Group, Others).  

---


```
r - 4
w - 2
x - 1

700 o-rwx, g-rx, o-r
```


```
chown
chgrp
```

### Find Command

- Locates files and directories based on conditions like name, size, type, or permissions.  
- Example: `find /path -name "*.txt" -exec rm {} \;` finds and deletes all `.txt` files.  
- Super versatile and supports actions like deleting, copying, or executing commands.  

[find](https://www.redhat.com/en/blog/linux-find-command)


```bash
find ./ -type f -newermt "2024-12-06" ! -newermt "2024-12-07"


find ./ -type f -name "demo.txt" -newermt "2024-12-06" ! -newermt "2024-12-07" -exec cp {} ./copy_dir \;
```


file info

```
sample
demo
```
```bash
find ./ -iname "*.txt" -exec grep -l "sample" {} \;
./demo.txt
[ec2-user@ip-172-31-30-109 ~]$ cat demo.txt
sample
demo
```

---

### Cut Command  
- Used to extract sections of text or fields from files or command output.  
- Example: `cut -d ',' -f 2 file.csv` extracts the second field from a CSV file.  
- Works well with delimiters like tabs, spaces, or custom characters.  

[cut](https://www.baeldung.com/linux/cut-command)

---

### AWK Command  
- A text-processing tool that works with pattern matching and fields.  
- Example: `awk '{print $1}' file.txt` prints the first column of each line.  
- Powerful for data extraction, transformation, and analysis.  

[awk]([https://](https://www.freecodecamp.org/news/the-linux-awk-command-linux-and-unix-usage-syntax-examples/))
---


```bash
 awk -F ':'  '{print $1 $4}'  passwd
 awk -F ':'  'BEGIN{OFS=" - "} {print $1,$4}'  passwd
 awk -F ':'  'BEGIN{OFS=" - "} {print $1,$4,$NF}'  passwd
```

note: $0 - everything $1 - 1st coloumn and $NF - last coloumn

### Unix Sort Command  
- Sorts lines of text files alphabetically, numerically, or by fields.  
- Example: `sort -n file.txt` sorts numerically, while `sort -r` sorts in reverse.

[sort](https://www.redhat.com/en/blog/sort-command-linux)

```bash

# text asc
sort filename

# text desc

sort -r filename

# numbers 

sort -n filename

# unique values

sort -u filename

# months

sort -M filename
```
---

### Tar Command  
- Archives files and directories.  
- Example: `tar -cvf archive.tar file1 file2` creates an archive; `-xvf` extracts it.  
- Combine with `gzip` or `bzip2` for compression.

[tar](https://www.redhat.com/en/blog/taming-tar-command)

---

### Process Control Commands  

#### **Process Management Shortcuts**:  
- **`Ctrl + C`**: Terminates the running process.  
- **`Ctrl + Z`**: Suspends a running process.  

#### `jobs`  
- Lists background and suspended jobs.  

#### `fg`  
- Brings a background job to the foreground.  

#### `bg`  
- Resumes a suspended job in the background.  

#### `&`  
- Appends to run a command in the background. Example: `command &`.  

#### `nohup`  
- Runs a command immune to hangups (terminal closure). Example: `nohup command &`.  

#### `kill`  
- Sends a signal to terminate a process by PID. Example: `kill 1234`.  

#### `killall`  
- Terminates all processes matching a name. Example: `killall firefox`.  

#### `pkill`  
- Kills processes matching a regex pattern. Example: `pkill -9 sshd`.  

#### Signals:  
- `kill -15`: Graceful stop (default).  
- `kill -9`: Forceful stop.  
- `kill -1`: Reloads process configuration.  

---

### Process Monitoring Commands  

#### `ps`  
- Displays currently running processes. Example: `ps -e`.  

#### `ps -ef`  
- Extended full-format listing of all processes.  

#### `pgrep`  
- Finds PIDs matching a pattern. Example: `pgrep nginx`.  

#### `top`  
- Interactive real-time process viewer.  

#### `free`  
- Displays system memory usage.  

#### `uptime`  
- Shows how long the system has been running.  

#### `watch`  
- Repeats a command every X seconds. Example: `watch -n 2 df -h`.  

