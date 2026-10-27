# Linux Mastery: Tasks Organized by Command

Each command has one real-world task. Do each one hands-on, then try variations.

---

## 1. Navigation & File Management

| Command | Real-time task |
|---|---|
| `pwd`, `cd`, `ls -lah` | Navigate to `/var/log`, list files sorted by size (`ls -lSh`), and explain each column |
| `mkdir -p` | Create `project/{src,docs,tests,logs}` in one command |
| `touch` | Create 100 files (`touch file{1..100}.txt`), then change one file's timestamp |
| `cp -r`, `mv`, `rm -rf` | Back up a directory, rename it, and delete the original safely (use `-i` first) |
| `ln`, `ln -s` | Make a hard link and a symlink to a file, delete the original, and see what breaks |
| `stat` | Compare the inode, size, and timestamps of two files |
| `file`, `tree` | Identify the real type of unknown files and map a directory structure |
| `du -sh *`, `df -h` | Find which folder in `/var` uses the most space |
| `basename`, `dirname`, `realpath` | Extract the filename and directory from a long path in a script |

## 2. Viewing & Editing Files

| Command | Real-time task |
|---|---|
| `cat`, `tac` | Display a config file normally and in reverse |
| `less`, `more` | Search a 100MB log (`/error`, `n`, `N`) without loading it all |
| `head`, `tail`, `tail -f` | Watch `/var/log/syslog` live while you trigger events (like a failed SSH login) |
| `vim` / `nano` | Edit `/etc/hosts`: add an entry, search/replace, and save |
| `wc -l` | Count lines, words, and bytes in a log file |
| `tee` | Save command output to a file and show it on screen at once |
| `diff`, `cmp` | Compare a config file with its backup and spot the change |
| `strings` | Extract readable text from a binary file |

## 3. Searching

| Command | Real-time task |
|---|---|
| `find / -name "*.conf"` | Locate every config file under `/etc` |
| `find -size +100M` | Hunt down files over 100MB when the disk is full |
| `find -mtime -1` | List files modified in the last 24 hours (useful after a suspected breach) |
| `find -perm -4000` | Audit all SUID binaries on the system |
| `find -exec` / `xargs` | Delete all `.tmp` files older than 7 days |
| `locate`, `updatedb` | Instantly find a file by name, then refresh the index |
| `which`, `whereis`, `type` | Find where a command lives and whether it's an alias |
| `grep -rn "password" /etc` | Search recursively for a string with line numbers |
| `grep -E`, `-i`, `-v`, `-c` | Extract all ERROR lines, ignore case, exclude noise, count matches |

## 4. Text Processing

| Command | Real-time task |
|---|---|
| `awk '{print $1}'` | Pull the IP address column from an Nginx access log |
| `sort \| uniq -c \| sort -nr` | Show the top 10 IPs hitting your web server |
| `cut -d: -f1 /etc/passwd` | List all usernames |
| `sed 's/old/new/g'` | Replace a port number across a config file |
| `sed -i.bak` | Edit in place while keeping a backup |
| `tr 'a-z' 'A-Z'` | Convert text to uppercase, or delete characters with `tr -d` |
| `paste`, `join` | Merge two files side by side or by a common field |
| `column -t` | Format messy output into a clean table |
| `jq` | Parse a JSON API response (`curl ... \| jq '.data[].name'`) |

## 5. Users, Groups & Permissions

| Command | Real-time task |
|---|---|
| `useradd -m -s /bin/bash` | Create a user with a home directory and shell |
| `passwd`, `chage -l` | Set a password and force expiry after 30 days |
| `usermod -aG` | Add a user to the `sudo` or `docker` group |
| `groupadd`, `gpasswd` | Create a `devteam` group and manage its members |
| `userdel -r` | Remove a user along with their home directory |
| `id`, `whoami`, `groups`, `who`, `last` | See who's logged in and who logged in recently |
| `su -`, `sudo -l` | Switch users and list what sudo permits |
| `visudo` | Let one user run only `systemctl restart nginx` |
| `chmod 755`, `chmod u+x` | Make a script executable; lock a private key to `600` |
| `chown -R user:group` | Fix ownership of a web root |
| `umask` | Change default permissions for new files |
| `chmod +t`, `chmod g+s` | Build a shared folder where users can't delete each other's files |
| `setfacl -m u:bob:rw`, `getfacl` | Give one user access without changing the group |
| `lsattr`, `chattr +i` | Make a file immutable, so even root can't delete it |

## 6. Process Management

| Command | Real-time task |
|---|---|
| `ps aux`, `ps -ef --forest` | Find a process and its parent/child tree |
| `top`, `htop` | Sort by CPU and memory to find the culprit |
| `pgrep`, `pidof` | Get the PID of a process by name |
| `kill -15`, `kill -9`, `pkill`, `killall` | Gracefully stop a process, then force-kill a stubborn one |
| `jobs`, `bg`, `fg`, `&` | Pause a task with Ctrl+Z, background it, bring it back |
| `nohup`, `disown`, `screen`, `tmux` | Run a long task that survives logout |
| `nice`, `renice` | Lower the priority of a heavy backup job |
| `lsof -i :80`, `lsof -p PID` | See which process holds a port or file |
| `strace -p PID` | Trace what a hung process is doing |
| `uptime`, `w` | Read load averages and explain the three numbers |

## 7. Disk & Storage

| Command | Real-time task |
|---|---|
| `lsblk`, `blkid`, `fdisk -l` | Identify all disks, partitions, and UUIDs |
| `fdisk` / `parted` | Partition a new virtual disk |
| `mkfs.ext4`, `mkfs.xfs` | Format the partition |
| `mount`, `umount` | Mount it at `/data` |
| `/etc/fstab` + `mount -a` | Make it permanent and test without rebooting |
| `pvcreate`, `vgcreate`, `lvcreate` | Build an LVM volume |
| `lvextend -r`, `resize2fs` | Grow a volume online |
| `mkswap`, `swapon`, `swapoff` | Create a swap file and activate it |
| `mdadm --create` | Build RAID1, fail a disk (`--fail`), and rebuild |
| `fsck`, `e2fsck` | Repair a filesystem (unmounted) |
| `dd if=/dev/zero of=test bs=1M count=500` | Create a test file and benchmark write speed |
| `quota`, `edquota` | Limit a user to 500MB |
| `ncdu` | Interactively find what's filling the disk |

## 8. Archiving, Compression & Backup

| Command | Real-time task |
|---|---|
| `tar -czvf` / `-xzvf` | Compress and extract a website backup |
| `tar -tf` | List an archive without extracting |
| `gzip`, `bzip2`, `xz`, `zip`, `unzip` | Compare compression ratio and speed on the same file |
| `rsync -avz --delete` | Mirror a directory locally and to a remote server |
| `rsync --link-dest` | Build space-efficient incremental backups |
| `scp`, `sftp` | Copy a file to another machine |
| `md5sum`, `sha256sum` | Verify a downloaded ISO or backup's integrity |
| `dd`, `ddrescue` | Clone a disk or partition |

## 9. Package Management

| Command | Real-time task |
|---|---|
| `apt update && apt upgrade` | Patch the whole system |
| `apt install`, `apt remove`, `apt purge` | Install nginx, then remove it along with its configs |
| `apt search`, `apt show`, `apt-cache policy` | Compare available package versions |
| `dpkg -i`, `dpkg -l`, `dpkg -S` | Install a `.deb` file; find which package owns a file |
| `dnf install`, `dnf history undo` | Roll back a bad install (RHEL family) |
| `rpm -qa`, `rpm -qf`, `rpm -ql` | Query installed packages and their files |
| `add-apt-repository`, `apt-key` / `gpg` | Add a third-party repo securely |
| `snap`, `flatpak` | Install and manage a snap package |
| `make`, `make install` | Compile a tool from source |

## 10. Services & systemd

| Command | Real-time task |
|---|---|
| `systemctl status/start/stop/restart/reload` | Manage nginx or sshd |
| `systemctl enable --now` | Make a service start on boot and run it immediately |
| `systemctl list-units --failed` | Find broken services |
| `systemctl cat`, `systemctl edit` | Inspect and override a unit file |
| Write `/etc/systemd/system/myapp.service` | Run a Python/Node script as a service with `Restart=always` |
| `systemctl daemon-reload` | Apply your new unit file |
| `systemctl get-default`, `set-default` | Switch between GUI and multi-user target |
| `systemd-analyze blame` | Find what slows your boot |
| `journalctl -u nginx -f` | Follow one service's logs live |
| `journalctl --since "1 hour ago" -p err` | Show recent errors only |
| `journalctl -b -1` | Read logs from the previous boot (after a crash) |

## 11. Scheduling

| Command | Real-time task |
|---|---|
| `crontab -e`, `crontab -l` | Run a backup script daily at 2 AM |
| `/etc/cron.d`, `anacron` | Understand system crons and missed jobs |
| `at`, `atq`, `atrm` | Schedule a one-time reboot or task |
| systemd `.timer` | Recreate your cron job as a timer |
| `sleep`, `watch -n 2` | Repeat a command every 2 seconds (e.g. `watch df -h`) |

## 12. Networking

| Command | Real-time task |
|---|---|
| `ip a`, `ip r`, `ip link` | Show interfaces, IPs, and routes |
| `ip addr add` | Assign a temporary secondary IP |
| `nmcli`, `netplan apply` | Set a static IP permanently |
| `ping`, `traceroute`, `mtr` | Find where packets drop on a path |
| `ss -tulpn` | List every listening port and its process |
| `dig`, `nslookup`, `host` | Query A, MX, and NS records; trace DNS with `dig +trace` |
| `curl -I`, `curl -v`, `curl -X POST` | Inspect HTTP headers and test an API |
| `wget`, `wget -c` | Download and resume a large file |
| `nc` (netcat) | Test if a remote port is open; chat between two machines |
| `nmap` | Scan your own server for open ports |
| `tcpdump -i eth0 port 80` | Capture HTTP traffic and save to `.pcap` |
| `arp -a`, `ip neigh` | See devices on your local network |
| `hostnamectl` | Change the hostname permanently |
| `/etc/hosts`, `/etc/resolv.conf` | Override DNS locally |
| `iftop`, `nload`, `vnstat` | Watch bandwidth live and over time |
| `iperf3` | Measure throughput between two servers |

## 13. SSH & Remote Access

| Command | Real-time task |
|---|---|
| `ssh user@host` | Connect, then run a single remote command |
| `ssh-keygen`, `ssh-copy-id` | Set up passwordless login |
| `ssh-agent`, `ssh-add` | Load a key once for the whole session |
| `~/.ssh/config` | Create aliases like `ssh webserver` |
| `ssh -L 8080:localhost:80` | Local port-forward to reach a remote web app |
| `ssh -R`, `ssh -D` | Remote tunnel and SOCKS proxy |
| `ssh -J` | Hop through a bastion host |
| `sshd_config` | Disable root login and password auth, restart sshd |
| `sshfs` | Mount a remote directory locally |

## 14. Firewall & Security

| Command | Real-time task |
|---|---|
| `ufw allow 22/tcp`, `ufw enable` | Allow SSH and HTTP, deny the rest |
| `firewall-cmd --add-service=http --permanent` | Open a service (RHEL family) |
| `iptables -A INPUT ...`, `iptables -L -n -v` | Write and inspect raw rules |
| `iptables -t nat -A PREROUTING` | Forward port 80 to an internal server |
| `nft list ruleset` | Read modern nftables rules |
| `fail2ban-client status sshd` | See banned IPs after test failed logins |
| `lastb`, `last`, `/var/log/auth.log` | Review failed and successful logins |
| `getenforce`, `setenforce`, `semanage`, `restorecon` | Fix an SELinux denial |
| `aa-status`, `aa-complain` | Manage AppArmor profiles |
| `gpg --encrypt`, `--sign`, `--decrypt` | Encrypt a file for a recipient |
| `cryptsetup luksFormat` | Encrypt a partition |
| `openssl req`, `openssl x509 -text` | Create a self-signed certificate and read it |
| `auditctl -w /etc/passwd -p wa` | Alert when a critical file changes |
| `lynis audit system` | Get a hardening score and fix 5 findings |
| `certbot --nginx` | Get a free HTTPS certificate |

## 15. Monitoring & Performance

| Command | Real-time task |
|---|---|
| `free -h` | Interpret "available" vs "free" memory |
| `vmstat 2`, `iostat -x 2`, `mpstat -P ALL` | Spot CPU wait, swapping, or disk saturation |
| `sar -u`, `sar -r` | Review historical CPU and memory |
| `dstat`, `glances`, `btop` | One-screen live overview |
| `iotop` | Find which process is hammering the disk |
| `dmesg -T \| tail` | Check for hardware errors or OOM kills |
| `sysctl -a`, `sysctl -w vm.swappiness=10` | Tune a kernel parameter |
| `ulimit -n` | Raise the open-file limit for a busy service |
| `lscpu`, `lsmem`, `lspci`, `lsusb`, `dmidecode` | Inventory hardware |
| `perf top`, `strace -c` | Profile what a program spends time on |
| `time` | Benchmark a command's runtime |

## 16. Shell & Scripting Essentials

| Command | Real-time task |
|---|---|
| `echo`, `printf`, `read` | Build an interactive prompt script |
| `export`, `env`, `printenv`, `set` | Manage environment variables; edit `~/.bashrc` and `source` it |
| `alias`, `unalias` | Create shortcuts (e.g. `alias ll='ls -lah'`) |
| `history`, `!!`, `Ctrl+R` | Reuse past commands efficiently |
| `if`, `case`, `for`, `while` | Loop through a list of servers and ping each |
| `function` | Write a reusable `backup()` function |
| `$?`, `&&`, `\|\|` | Chain commands conditionally |
| `set -euo pipefail`, `trap` | Make a script fail safely and clean up |
| `bash -x`, `shellcheck` | Debug and lint scripts |
| `getopts` | Add `-f file -v` flags to a script |
| `test`, `[[ ]]` | Check whether a file or directory exists |
| `date +%F_%H%M` | Timestamp backup filenames |
| `mktemp` | Create safe temporary files |
| `<<EOF` (here-doc) | Write a multi-line config from a script |
| `2>&1`, `/dev/null` | Redirect errors and silence output |

## 17. Containers, Git & DevOps

| Command | Real-time task |
|---|---|
| `docker run -d -p 80:80 nginx` | Launch a web server in seconds |
| `docker ps`, `logs`, `exec -it`, `stop`, `rm` | Manage and debug containers |
| `docker build -t myapp .` | Write a Dockerfile and build it |
| `docker volume`, `docker network` | Persist data and connect containers |
| `docker compose up -d` | Run app + database together |
| `unshare`, `nsenter`, `ls /sys/fs/cgroup` | See what containers are really made of |
| `git init`, `add`, `commit`, `log` | Version your scripts and dotfiles |
| `git branch`, `merge`, `rebase`, `stash` | Practice a branching workflow |
| `git clone`, `push`, `pull` | Sync with GitHub |
| `ansible all -m ping`, `ansible-playbook` | Configure multiple servers from one playbook |
| `terraform init/plan/apply` | Provision a cloud VM as code |
| `virsh`, `qemu-img` | Manage KVM virtual machines |

## 18. Kernel, Boot & Recovery

| Command | Real-time task |
|---|---|
| `uname -a`, `cat /etc/os-release` | Identify kernel and distro |
| `lsmod`, `modprobe`, `modinfo`, `rmmod` | Load and unload a kernel module |
| `grub-mkconfig`, `update-grub`, `grub-install` | Rebuild GRUB after breaking it |
| `chroot` (from a live USB) | Repair an unbootable system |
| `mount -o remount,rw /` | Fix a read-only root in rescue mode |
| `dracut`, `update-initramfs -u` | Rebuild the initramfs |
| `udevadm info`, `udevadm monitor` | Watch devices as you plug them in |
| `/proc`, `/sys` exploration | Read `cat /proc/cpuinfo`, `/proc/meminfo`, `/proc/PID/status` |
| `reboot`, `shutdown -r +5`, `poweroff` | Schedule a reboot with a warning message |
| `wall`, `write`, `mesg` | Broadcast a message to logged-in users |

---

## How to Practice Each Command

1. **Run it plain**, then read `man` for 3 flags you haven't used.
2. **Break it deliberately**: wrong permissions, a full disk, a bad config.
3. **Combine it with pipes**: `ps aux | grep nginx | awk '{print $2}' | xargs kill`.
4. **Script it** once you can do it by hand.
5. **Add it to your cheat sheet** with one real example.

If you'd like, I can turn this into a downloadable checklist (Excel or Markdown) with a checkbox for each command, or build a 30-day plan around it.
