# Linux Cheat Sheet

**About:** This repository contains a progressively structured, enterprise-grade Linux command and scripting cheat sheet. Extracted from professional reference materials, it guides users from basic file navigation and terminal shortcuts to advanced text processing (`sed`/`awk`/Regex), network diagnostics, package management, disk manipulation, and firewall configuration.
**Tags:** `#Linux` `#SysAdmin` `#Bash` `#Networking` `#DevOps` `#CheatSheet` `#Regex`

---

## Table of Contents
* [Level 1: Basic Navigation & Bash Shortcuts](#level-1-basic-navigation--bash-shortcuts)
* [Level 2: File Searching, Viewing & Operations](#level-2-file-searching-viewing--operations)
* [Level 3: Hardware, System & Disk Monitoring](#level-3-hardware-system--disk-monitoring)
* [Level 4: User Management, Auditing & Permissions](#level-4-user-management-auditing--permissions)
* [Level 5: Process Management & Job Control](#level-5-process-management--job-control)
* [Level 6: I/O Redirection & Text Manipulation](#level-6-io-redirection--text-manipulation)
* [Level 7: Advanced Stream Editing (sed) & Regex](#level-7-advanced-stream-editing-sed--regex)
* [Level 8: Networking, Routing & File Transfer](#level-8-networking-routing--file-transfer)
* [Level 9: Firewalls & Security Configuration](#level-9-firewalls--security-configuration)
* [Level 10: Package Management & Archiving](#level-10-package-management--archiving)
* [Level 11: Disks, ISOs & System Power](#level-11-disks-isos--system-power)

---

## Level 1: Basic Navigation & Bash Shortcuts

Explore the filesystem, manage directories, and navigate the terminal efficiently.

**Bash Shortcuts & Keyboard Navigation**
Speed up your terminal workflow using default readline shortcuts.
```bash
CTRL-a
CTRL-e
CTRL-u
CTRL-k
CTRL-r
CTRL-c
CTRL-z
```
*   `CTRL-a`: Move the cursor to the start of the line.
*   `CTRL-e`: Move the cursor to the end of the line.
*   `CTRL-u`: Cut text from the cursor to the start of the line.
*   `CTRL-k`: Cut text from the cursor to the end of the line.
*   `CTRL-r`: Search backward through command history.
*   `CTRL-c`: Stop/interrupt the current running command.
*   `CTRL-z`: Suspend/sleep the current foreground program.

**List Directory Contents**
Lists files and directories with options to format the output.
```bash
ls --file-type
ls -alR
```
*   `--file-type`: Appends a type indicator to entries.
*   `-a`: Shows all files, including hidden ones.
*   `-l`: Uses a long listing format detailing permissions and ownership.
*   `-R`: Lists subdirectories recursively.

**Change and Print Directory**
Navigates the filesystem tree and displays paths.
```bash
cd /etc
cd ../..
cd ~
pwd
readlink -f example
```
*   `/etc`: Changes to the specific absolute path.
*   `../..`: Moves up two directory levels.
*   `~`: Navigates to the current user's home directory.
*   `pwd`: Outputs the present working directory.
*   `readlink -f`: Canonicalizes by following every symlink to get the absolute path.

**Create, Copy, and Move Files**
```bash
touch newfile.txt
mkdir new_folder
cp -r source_dir destination_dir
mv example.txt ~/Documents
```
*   `touch`: Creates an empty file or updates timestamps.
*   `cp -r`: Copies directories and their contents recursively.
*   `mv`: Moves a file to a new location or renames it.

**Remove and Delete Files**
```bash
rm -rf directory
rmdir example
trash example.txt
shred example.txt
```
*   `-r`: Removes directories and contents recursively.
*   `-f`: Forces removal without prompting.
*   `trash`: Safely moves a file to the system trash.
*   `shred`: Permanently and securely deletes a file.

---

## Level 2: File Searching, Viewing & Operations

Locate files efficiently and peek into their contents.

**Search for Files**
Locates files matching specific parameters or patterns.
```bash
find /home/john -name 'prefix*'
find /dir/ -mmin 5
whereis command
locate file
```
*   `-name`: Searches for files matching the given string prefix.
*   `-mmin num`: Finds files modified less than `num` minutes ago.
*   `whereis`: Locates the binary, source, or manual page for a command.

**View File Contents**
Reads and concatenates files onto the standard output or a pager.
```bash
cat file1 file2
less file
head file
tail -f file
```
*   `cat`: Concatenates and outputs full file contents.
*   `less`: Views the file in a paginated, scrollable interface.
*   `head` / `tail`: Displays the first or last 10 lines of a file.
*   `-f`: Continually follows and outputs new lines as the file grows.

**Identify File Type**
```bash
file file1
```
*   Determines the data type of a specific file (e.g., ASCII text, ELF executable).

---

## Level 3: Hardware, System & Disk Monitoring

Inspect kernel logs, manage memory, and check performance metrics.

**Hardware and Kernel Info**
```bash
dmesg
lspci -tv
lsusb -tv
dmidecode
```
*   `dmesg`: Displays kernel ring buffer messages.
*   `lspci` / `lsusb -tv`: Shows a tree-like view for PCI and USB devices.
*   `dmidecode`: Dumps system DMI/SMBIOS hardware information.

**System Performance & Memory**
Shows processor metrics, free memory, and I/O wait times.
```bash
cat /proc/cpuinfo
free -h
vmstat 1
mpstat 1
iostat 1
```
*   `free -h`: Displays free memory in a human-readable format.
*   `vmstat 1`: Updates virtual memory statistics every 1 second.
*   `mpstat 1`: Displays processor-related statistics.
*   `iostat 1`: Displays input/output statistics for devices and partitions.

**Disk Usage and Health**
```bash
df -h
du -sh
fdisk -l
hdparm -tT /dev/sda
badblocks -s /dev/sda
```
*   `df -h`: Shows free/used space on filesystems.
*   `du -sh`: Shows the total summary size of the current directory.
*   `fdisk -l`: Lists disk partition sizes and types.
*   `hdparm -tT`: Performs cache and device read speed tests.
*   `badblocks -s`: Tests for unreadable blocks on the specified disk.

---

## Level 4: User Management, Auditing & Permissions

Manage user accounts, groups, and modify system access controls.

**User Information & Auditing**
Queries identities and checks account integrity.
```bash
id
groups
w
last
pwck
grpck
```
*   `id` / `groups`: Finds your current UID, GID, and group memberships.
*   `w` / `last`: Displays currently logged-in users and recent logins.
*   `pwck` / `grpck`: Verifies the integrity of password and group configuration files.

**User Account Creation & Ownership**
```bash
useradd -c "John Smith" -m john
groupadd test
sudo chown user2:group2 foo
chgrp 2 foo
```
*   `-c` / `-m`: Adds a comment (full name) and creates the user's home directory.
*   `chown`: Simultaneously changes the user and group ownership of a file.

**Change Permissions (chmod/umask)**
```bash
chmod 755 filename
chmod +x foo
umask
```
*   `755`: Grants rwx (7) to owner, rx (5) to group, rx (5) to world.
*   `+x`: Grants execute permissions to all users symbolically.

---

## Level 5: Process Management & Job Control

Monitor, control, and terminate active system processes.

**List and Monitor Processes**
```bash
ps -ef | grep processname
ps -e -o pid,args --forest
top
htop
pstree
```
*   `-ef`: Displays all system processes in detail.
*   `--forest` / `pstree`: Displays a visual tree of processes and their relationships.
*   `top` / `htop`: Interactive process viewers and managers.

**Terminate Processes**
```bash
kill -9 98989
killall processname
pkill name
```
*   `-9`: Kills the PID immediately (SIGKILL).
*   `killall`: Kills all processes matching the specific exact name.

**Background Jobs and Multiplexing**
```bash
program &
bg
fg
watch -n 5 'ntpq -p'
screen -r
```
*   `&` / `bg` / `fg`: Manages background and foreground execution.
*   `watch -n 5`: Re-executes a command every 5 seconds.
*   `screen -r`: Resumes an existing, detached terminal screen session.

---

## Level 6: I/O Redirection & Text Manipulation

Pipe data between commands and filter text efficiently.

**Input/Output Redirection**
```bash
cmd > file
cmd >> file
cmd 2> file
cmd &> file
cmd1 <(cmd2)
```
*   `>` / `>>`: Redirects and overwrites or appends standard output to a file.
*   `2>` / `&>`: Redirects error output (stderr) or *both* stdout and stderr.
*   `<()`: Passes the output of `cmd2` as a file input to `cmd1`.

**Text Searching (grep)**
```bash
grep ^Aug /var/log/messages
grep [0-9] /var/log/messages
grep Aug -R /var/log/*
```
*   `^Aug`: Matches lines starting specifically with "Aug".
*   `-R`: Searches files inside the specified directory recursively.

**Text Sorting, Filtering & Processing**
```bash
sort file1 file2 | uniq -u
comm -3 file1 file2
awk 'NR%2==1' example.txt
echo a b c | awk '{print $1,$3}'
echo 'test' | tr '[:lower:]' '[:upper:]'
```
*   `uniq -u`: Displays only unique strings across the files.
*   `comm -3`: Compares two files and deletes lines appearing in both.
*   `awk`: Extracts specific columns (`$1,$3`) or odd-numbered lines (`NR%2==1`).
*   `tr`: Translates character sets (e.g., lowercase to uppercase).

---

## Level 7: Advanced Stream Editing (sed) & Regex

Perform line-by-line programmatic text transformations.

**Regular Expressions (Regex) Reference**
Use these operators with `grep`, `sed`, and `awk` for powerful pattern matching.
*   `.` : Any single character
*   `^` : Start of a line
*   `$` : End of a line
*   `?` : Match preceding item zero or one time
*   `*` : Match preceding item zero or more times
*   `+` : Match preceding item one or more times
*   `{2}` : Match preceding item exactly two times
*   `[A,B]` : Match A or B
*   `[1-3]` : Match all digits 1 to 3
*   `\s` : Space
*   `\t` : Tab
*   `\n` : Newline

**Basic Searching and Replacing**
```bash
sed 's/closed/open/g'
sed '/code/! s/closed/open/g'
sed -e 's/ *$//' example.txt
```
*   `s/old/new/g`: Replaces 'old' with 'new' globally across the line.
*   `/code/!`: Executes the substitution ONLY on lines *not* containing "code".
*   `s/ *$//`: Removes trailing whitespace at the end of every line.

**Deleting Lines and Printing Ranges**
```bash
sed '1d;$d'
sed '/^$/d' example.txt
sed -n '3,7 p'
```
*   `1d;$d`: Deletes the first (`1`) and last (`$`) lines of the file.
*   `/^$/d`: Deletes all empty lines using Regex.
*   `3,7 p`: Selects lines 3 through 7, and prints them.

**Advanced Pattern & Hold Space Manipulations**
```bash
sed -n -e '/[Oo]pen/h' -e '/[Oo]pen/d' -e '/projects/ G;p'
sed = FILE | sed 'N ; s/\n/\t/'
```
*   `h` / `G`: Copies to the hold space and appends it back (cut and paste).
*   `=` / `N`: Prints current line numbers and merges lines together.

---

## Level 8: Networking, Routing & File Transfer

Inspect local interfaces, configure routing, trace paths, and transfer data securely.

**Interface Configuration & Routing**
```bash
ifconfig eth0 192.168.1.1 netmask 255.255.255.0
ifup eth0
ifdown eth0
dhclient eth0
route -n
route add -net 192.168.0.0 netmask 255.255.0.0 gw 192.168.1.1
nmcli connection show
```
*   `ifup` / `ifdown`: Brings a network interface up or down.
*   `dhclient`: Renews the IP address via DHCP for the specified interface.
*   `route -n`: Displays the local IP routing table natively.
*   `route add`: Configures a static route through a specific gateway (`gw`).
*   `nmcli`: Command-line tool to manage NetworkManager connections.

**Diagnostics, DNS & Packet Capturing**
```bash
ping host
traceroute www.ya.ru
dig -x IP_ADDRESS
netstat -nutlp
tcpdump -i eth0 'port 80'
```
*   `traceroute`: Traces the network path/hops to a designated host.
*   `netstat -nutlp`: Displays active network statistics and listening TCP/UDP ports.
*   `tcpdump`: Captures packets exclusively on a specified interface/port.

**Network File Transfers & Sharing**
```bash
wget http://example.com/file
scp server:/var/www/*.html /tmp
smbclient -L ip_addr/hostname
```
*   `wget`: Downloads a file from a specified network location.
*   `scp`: Securely copies files over SSH.

---

## Level 9: Firewalls & Security Configuration

Secure the host system using Firewalld and iptables rules.

**Firewall-cmd: Zone and Service Management**
```bash
firewall-cmd --get-active-zones
firewall-cmd --add-port=123/tcp --zone=home --permanent
firewall-cmd --add-service murmur --zone=home
firewall-cmd --reload
```
*   `--add-port` / `--add-service`: Explicitly permits TCP traffic on ports or registered services.
*   `--permanent`: Ensures changes persist across reloads.
*   `--reload`: Activates any newly added permanent rules immediately.

**iptables: Traffic Filtering and NAT**
```bash
iptables -t filter -nL
iptables -t filter -A INPUT -p tcp --dport telnet -j ACCEPT
iptables -t nat -A POSTROUTING -o eth0 -j MASQUERADE
```
*   `-A INPUT -j ACCEPT`: Appends a rule to allow incoming connections.
*   `-A POSTROUTING -j MASQUERADE`: Enables Network Address Translation (NAT) for outgoing packets.

---

## Level 10: Package Management & Archiving

Install software and compress/extract files across different Linux distributions.

**Archiving and Compression (tar, zip)**
```bash
tar -cvfz archive.tar.gz dir1
tar -xvf archive.tar -C /tmp
zip -r file1.zip file1 file2 dir1
unzip file1.zip
```
*   `-c` / `-x`: Creates a new archive (`c`) or extracts an existing one (`x`).
*   `-v` / `-f` / `-z`: Verbose output (`v`), specifies filename (`f`), and compresses via gzip (`z`).
*   `-C`: Extracts files into the designated target directory.

**Red Hat / CentOS / Fedora (RPM & YUM)**
```bash
rpm -ivh package.rpm
rpm -qa | grep httpd
rpm -e package_name.rpm
yum install package_name
yum update
```
*   `rpm -ivh`: Installs an RPM package with verbose output and a hash progress bar.
*   `rpm -qa`: Queries and lists all installed packages on the system.
*   `rpm -e`: Erases (uninstalls) a package.
*   `yum install` / `update`: Downloads and installs a package and its dependencies, or updates the whole system.

**Debian / Ubuntu / OpenSUSE (General Syntax)**
```bash
sudo apt search example
sudo apt install example
sudo zypper install example
```
*   Depending on the distribution, replace `yum` with `apt` (Debian/Ubuntu), `dnf` (newer Fedora), or `zypper` (OpenSUSE) to interact with repositories.

---

## Level 11: Disks, ISOs & System Power

Manage runlevels, reboot the system, and manipulate raw disk images.

**Power and Boot Management**
```bash
shutdown -h now
reboot
init 0
```
*   `shutdown -h now`: Halts the system and powers off immediately.
*   `reboot`: Restarts the system.
*   `init 0`: Changes the runlevel to 0 (halt/shutdown).

**ISO Creation and CD/DVD Burning**
```bash
mkisofs /dev/cdrom > cd.iso
cdrecord -v dev=/dev/cdrom cd.iso
cd-paranoia -B
```
*   `mkisofs`: Creates an ISO image file from a directory or device.
*   `cdrecord`: Burns an ISO image directly to an optical drive.
*   `cd-paranoia -B`: Rips audio tracks from a CD to WAV files.

**Raw Disk Cloning and MBR Manipulation**
```bash
dd if=/dev/hda of=/dev/fd0 bs=512 count=1
```
*   `dd`: Performs low-level, bit-for-bit data copying.
*   `if=` / `of=`: Specifies the input file (source) and output file (destination).
*   `bs=512 count=1`: Copies exactly 512 bytes once (useful for backing up the Master Boot Record).
