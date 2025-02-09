# **Introduction**

 Exploiting vulnerabilities in the kernel or kernel modules is a common method of privilege escalation. This typically requires an unpatched kernel with known vulnerabilities that allow users to escalate privileges.
 ---


## **1. Basic System Information**

  Kernel Version : 

      $ uname -r
    
      $ cat /proc/version

  OS Release Information : 

      $ cat /etc/os-release
  
      $ cat /etc/redhat-release     - For RHEL-based distributions
  
      $ cat /etc/*-release

  Distribution Information : 
  
      $ lsb_release -a


## **2. Advanced System Details**


  System Hardware Details : 

      $ dmesg | grep -i linux

  System Information Summary : 

      $ hostnamectl
  
      $ hostname

  System Uptime and Load : 

      $ uptime

  Boot Logs for Kernel Messages : 

      $ journalctl -k 
  
      $ sysctl -a | grep kernel 


## **3. Kernel Package Management**

 
  Query Installed Kernel Packages : 

      $ rpm -q kernel 

  Query All Kernel-Related Packages : 

      $ rpm -qa | grep kernel

  List Installed Kernel Packages (Debian-based) :

      $ dpkg -l | grep kernel
  


## **4. Kernel and Boot Information**

  
  Kernel Boot Messages :

      $ dmesg | grep -i linux
  
      $ dmesg | grep -i kernel

  Kernel Files in /boot :

      $ ls /boot | grep vmlinuz-


## **5. Additional Useful Commands**


  List Active Kernel Modules :

      $ lsmod

  View Kernel Command Line Parameters  :

      $ cat /proc/cmdline

  Check Kernel Configuration (If Available) :

       $ zcat /proc/config.gz | grep CONFIG_


# **Checking Vulnerable Kernel Versions**

## Overview 

This script extracts and lists vulnerable Linux kernel versions based on the data from the [lucyoa/kernel-exploits](https://github.com/lucyoa/kernel-exploits) repository. It retrieves the README file and filters out kernel versions mentioned as vulnerable.
---

**Usage :**

    $ curl https://raw.githubusercontent.com/lucyoa/kernel-exploits/refs/heads/master/README.md 2>/dev/null | grep "Kernels: " | cut -d ":" -f 2 | cut -d "<" -f 1 | tr -d "," | tr ' ' '\n' | grep -v "^\d\.\d$" | sort -u -r | tr '\n' ' '  

**Check for a Specific Kernel Version :**

    $ curl https://raw.githubusercontent.com/lucyoa/kernel-exploits/refs/heads/master/README.md 2>/dev/null | grep "Kernels: " | cut -d ":" -f 2 | cut -d "<" -f 1 | tr -d "," | tr ' ' '\n' | grep -v "^\d\.\d$" | sort -u -r | tr '\n' ' ' | grep 3.8.2
