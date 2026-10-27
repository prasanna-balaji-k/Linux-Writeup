# Linux Mastery: Hands-On Task Roadmap

**Setup first:** Use a VM (VirtualBox/VMware), WSL2, or a cheap cloud VPS. Ubuntu/Debian is a good start, and Rocky/AlmaLinux later for the RHEL family. Break things on purpose, since that's where the learning happens.

---

## Phase 1: Foundations (Week 1-2)

**Navigation & files**
- Create a project directory tree with one command (`mkdir -p`)
- Copy, move, rename, and delete files and directories, then recover from a mistake
- Find all `.log` files larger than 10MB (`find`)
- Create hard links and symlinks and observe the difference
- Compare `ls -l` output and explain every column

**Viewing & editing**
- Read a large log with `less`, `head`, `tail -f`
- Edit a config file in `vim` or `nano` (save, quit, search, replace)
- Complete `vimtutor`

**Help system**
- Learn a new command using only `man`, `--help`, and `info`

---

## Phase 2: Users, Permissions & Processes (Week 2-3)

**Users & groups**
- Create users, groups, and add a user to a group (`useradd`, `usermod`, `groupadd`)
- Set password expiry policy (`chage`)
- Configure `sudo` access with `visudo` for one specific command only
- Lock/unlock an account, then delete one cleanly

**Permissions**
- Set up a shared directory where a team can read/write but others can't
- Use `chmod` in numeric and symbolic modes
- Apply SUID, SGID, and sticky bit, and explain a real use of each
- Use ACLs (`setfacl`, `getfacl`)
- Change ownership recursively with `chown`

**Processes**
- Find and kill a runaway process (`ps`, `top`, `htop`, `kill`, `pkill`)
- Run jobs in the background/foreground (`&`, `fg`, `bg`, `nohup`)
- Change process priority (`nice`, `renice`)
- Explore `/proc` for a running process

---

## Phase 3: Text Processing & Shell Scripting (Week 3-5)

**Command-line power tools**
- Count unique IPs in an access log, sorted by frequency (`awk`, `sort`, `uniq`)
- Extract error lines with `grep -E`, then bulk-replace text with `sed`
- Chain commands with pipes, redirects, and `tee`
- Use `cut`, `tr`, `xargs`, `wc`, `diff`

**Bash scripting projects**
- Write a script that backs up a directory with a timestamp
- Write a script that checks disk usage and emails/logs a warning above 80%
- Write a user-creation script that reads from a CSV
- Build a log-rotation or old-file cleanup script
- Use variables, loops, conditionals, functions, and `getopts`
- Add error handling (`set -euo pipefail`, `trap`)
- Debug a script using `bash -x`

**Automation**
- Schedule a script with `cron`
- Do the same with a `systemd` timer
- Use `at` for one-time jobs

---

## Phase 4: System Administration (Week 5-8)

**Package management**
- Install, remove, and update software (`apt`/`dnf`)
- Add a third-party repository and GPG key
- Compile software from source (`./configure && make && make install`)
- Find which package owns a file

**Services with systemd**
- Start, stop, enable, and check a service (`systemctl`)
- Write your own `.service` unit file for a script or app
- Read logs with `journalctl` (filter by unit, time, priority)
- Change the default boot target

**Disk & storage**
- Add a new virtual disk, partition it (`fdisk`/`parted`), format it (`mkfs`), and mount it
- Make the mount persistent via `/etc/fstab`
- Set up LVM: create PV, VG, LV, then extend a volume online
- Create and activate swap space
- Set up software RAID (`mdadm`) and simulate a disk failure
- Set disk quotas for a user
- Check and repair a filesystem (`fsck`)

**Boot & recovery**
- Understand the boot process (BIOS/UEFI, GRUB, kernel, init)
- Reset a forgotten root password via GRUB
- Fix a broken `/etc/fstab` using rescue mode
- Rebuild/reinstall GRUB

**Logs & monitoring**
- Read `/var/log/*` files and understand `rsyslog`
- Configure `logrotate` for a custom app
- Monitor with `vmstat`, `iostat`, `sar`, `free`, `df`, `du`, `lsof`
- Find what is eating CPU, memory, or disk I/O

---

## Phase 5: Networking (Week 8-10)

**Core tasks**
- Configure a static IP (Netplan or NetworkManager/`nmcli`)
- Diagnose connectivity layer by layer (`ping`, `traceroute`, `mtr`, `ip`, `ss`, `dig`, `nslookup`)
- Edit `/etc/hosts` and `/etc/resolv.conf`
- See which process is listening on which port (`ss -tulpn`)
- Capture and analyze traffic with `tcpdump` (and Wireshark)
- Transfer files with `scp`, `rsync`, `curl`, `wget`

**SSH (very important)**
- Set up key-based login and disable password authentication
- Harden `sshd_config` (disable root login, change port, limit users)
- Use `~/.ssh/config` with aliases
- Create SSH tunnels (local, remote, dynamic/SOCKS)
- Set up a jump host (bastion)

**Firewall**
- Configure `ufw` or `firewalld`
- Write raw `iptables`/`nftables` rules (allow SSH/HTTP, drop the rest)
- Set up NAT/port forwarding
- Install and configure `fail2ban` and watch it block an attacker

**Network services**
- Run a DHCP server and DNS server (`bind9` or `dnsmasq`)
- Set up NFS and Samba shares
- Configure NTP/`chrony` time sync

---

## Phase 6: Servers & Real-World Services (Week 10-13)

- Host a website with **Nginx** or **Apache** (virtual hosts, reverse proxy)
- Add free HTTPS with Let's Encrypt (`certbot`)
- Install and secure **MySQL/PostgreSQL**, then schedule backups
- Set up a mail relay (Postfix) or a self-hosted app like Nextcloud
- Deploy a Node/Python app behind Nginx as a systemd service
- Set up an FTP/SFTP server with chrooted users
- Configure load balancing with HAProxy or Nginx
- Build a LAMP/LEMP stack from scratch

---

## Phase 7: Security & Hardening (Week 13-15)

- Run a security audit with `lynis`
- Check open ports with `nmap` against your own machine
- Configure SELinux (RHEL) or AppArmor (Ubuntu): fix a denial, change a context
- Set up `auditd` to track file access
- Enforce password policy with PAM
- Enable automatic security updates
- Set up two-factor authentication for SSH
- Encrypt a disk or partition with LUKS
- Use GPG to encrypt/sign files
- Detect intrusions with `AIDE` or `rkhunter`
- Review failed logins (`lastb`, `/var/log/auth.log`)

---

## Phase 8: Automation, DevOps & Containers (Week 15-20)

**Containers & virtualization**
- Install Docker, run containers, write a Dockerfile, use volumes and networks
- Use Docker Compose for a multi-container app
- Create VMs with KVM/QEMU and `virsh`
- Explore namespaces and cgroups (what containers are made of)

**Configuration management & IaC**
- Write an Ansible playbook to configure 3 servers identically
- Provision a cloud VM with Terraform
- Manage dotfiles with Git

**Git & CI/CD**
- Use Git from the CLI (branch, merge, rebase, resolve conflicts)
- Build a simple pipeline (GitHub Actions or Jenkins) that deploys to your server

**Monitoring stack**
- Install Prometheus + Grafana + node_exporter
- Centralize logs with the ELK stack or Loki
- Set up an alert (CPU > 90% sends a notification)

---

## Phase 9: Advanced & Kernel-Level (Ongoing)

- Compile and boot a custom kernel
- Load/unload kernel modules (`modprobe`, `lsmod`), tune with `sysctl`
- Trace a program with `strace`, `ltrace`, `perf`
- Debug a hung system using `dmesg` and `/proc`
- Understand `/sys`, `udev` rules, and device files
- Write a systemd-based custom boot service
- Performance tuning: I/O schedulers, swappiness, ulimits
- Explore eBPF tools (`bpftrace`)
- Build a minimal Linux (Linux From Scratch) as a capstone

---

## Real-World Troubleshooting Drills

Practice these scenarios regularly. Break the system, then fix it:

1. Server is slow, so find the bottleneck (CPU, RAM, disk, network)
2. Disk is 100% full, so find what's consuming it and clean up safely
3. Can't SSH in, so debug from the console side
4. Service won't start, so diagnose with `journalctl` and `systemctl status`
5. System won't boot after an `fstab` or kernel change
6. Accidentally ran `chmod -R 777 /` or deleted a critical file, so recover
7. Website is down, so trace it from DNS to firewall to web server to app
8. Out-of-memory killer terminated a process, so find out why

---

## Capstone Projects

- **Home lab server:** DNS + DHCP + web + file share + VPN (WireGuard) + monitoring
- **Hardened web host** with automated backups, firewall, fail2ban, and HTTPS
- **Fully automated deployment:** Git push, CI pipeline, Ansible, live app
- **Personal cloud:** Nextcloud + reverse proxy + encrypted storage

---

## Tips for Mastery

- Do each task by hand first, then script or automate it
- Keep a **notes/cheat-sheet repo** on GitHub
- Use free labs: OverTheWire (Bandit), TryHackMe, KodeKloud, Linux Journey
- Consider certifications to structure your learning: **LFCS, RHCSA, Linux+**
- Practice on the CLI only, with no GUI crutches

I can turn this into a downloadable checklist or a week-by-week study plan with time estimates if that would help.
