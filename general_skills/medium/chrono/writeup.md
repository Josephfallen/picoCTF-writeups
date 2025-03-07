# Chrono Writeup

## Introduction

This write-up explains how to retrieve scheduled cron jobs on a remote Linux system. The approach follows an investigative process using basic system administration commands to discover hidden flags in a Capture the Flag (CTF) challenge.

## Steps to Retrieve the Cron Job Information

### 1. Connecting to the Remote Machine
To begin, we established an SSH connection to the target system using the provided credentials:
```bash
ssh saturn.picoctf.net -p <portnumber> -l picoplayer
```
After entering the correct password, we successfully logged into the remote machine.

### 2. Exploring the System
Once logged in, we listed the files in the home directory:
```bash
ls
```
No relevant files were found, so we proceeded to investigate system services.

### 3. Checking for a Service Named "Chrono"
We initially tried checking for a service named "chrono" using `systemctl`:
```bash
systemctl status chrono
```
However, we encountered an error indicating that the system was not using `systemd`.

### 4. Attempting to Use sudo Privileges
We attempted to run the command with `sudo`:
```bash
sudo systemctl status chron
```
This resulted in an error since the `picoplayer` user did not have sudo privileges.

### 5. Checking Cron Jobs
Since system services were not accessible, we turned to cron jobs, which are used to schedule tasks on Linux. We listed the user's cron jobs using:
```bash
crontab -l
```
This returned "no crontab for picoplayer," indicating there were no user-specific cron jobs.

### 6. Examining System-wide Cron Jobs
Since no user-specific cron jobs were found, we checked the system-wide crontab file:
```bash
cat /etc/crontab
```
This file contained the hidden flag:
```bash
picoCTF{Sch3DUL7NG_T45K3_L1NUX_9d5cb744}
```

## How We Discovered the Solution
When faced with the challenge, we researched methods to list cron jobs. A helpful guide from Linode provided insight into different ways to examine scheduled tasks on a Linux system:
[How to List Cron Jobs](https://www.linode.com/docs/guides/how-to-list-cron-jobs/).
This guided us towards checking system-wide cron jobs using `/etc/crontab`, which ultimately led us to the flag.

## Conclusion
This challenge demonstrated the importance of checking various task scheduling mechanisms in Linux. When investigating scheduled tasks, both user-specific (`crontab -l`) and system-wide (`/etc/crontab`) cron jobs should be considered. Understanding these system administration concepts is crucial for both cybersecurity challenges and real-world system management.

