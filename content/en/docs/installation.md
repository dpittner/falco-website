---
title: Install
description: Setting up Falco on a Linux system
weight: 3
---

Falco is a Linux security tool that uses system calls to secure and monitor a system. 

{{< info >}}

The Falco Project does not suggest running Falco on top of Kubernetes but rather beside Kubernetes on the Linux host with systemd. 

See this [blog post](../blog/falco-and-kubernetes/) for more information.

If you would like to run Falco in Kubernetes with a tool like Kind, Minikube, or Helm please see the [third party integrations](../third-party)

{{< /info >}}



If Falco is installed using the package manager artifacts below, you will have the following in place.

 - Falco userspace program scheduled and watched via `systemd`
 - Falco driver installed via package manager (either kernel module or eBPF depending on host)
 - Sane and default configuration file installed in `/etc/falco`

## Installing

### Debian/Ubuntu

1. Trust the falcosecurity GPG key, configure the apt repository, and update the package list:

    ```bash
    curl -s https://falco.org/repo/falcosecurity-3672BA8F.asc | apt-key add -
    echo "deb https://dl.bintray.com/falcosecurity/deb stable main" | tee -a /etc/apt/sources.list.d/falcosecurity.list
    apt-get update -y
    ```

2. Install kernel headers:

    ```shell
    apt-get -y install linux-headers-$(uname -r)
    ```

3. Install Falco:

    ```shell
    apt-get install -y falco
    ```
   
    Falco, the kernel module driver, and a default configuration are now installed. 
    Falco is being ran as a systemd unit.   

    See [running](../running) for information on how to manage, run, and debug with Falco. 
       

4. Uninstall Falco:

    ```shell
    apt-get remove falco
    ```

### CentOS/RHEL/EC2 Linux/Fedora

1. Trust the falcosecurity GPG key and configure the yum repository:

    ```shell
    rpm --import https://falco.org/repo/falcosecurity-3672BA8F.asc
    curl -s -o /etc/yum.repos.d/falcosecurity.repo https://falco.org/repo/falcosecurity-rpm.repo
    ```
   
    > **Note** — The following command is required only if DKMS is not available in the distribution. You can verify if DKMS is available using `yum list dkms`. If necessary install it using: `yum install epel-release`

2. Install kernel headers:

    ```shell
    yum -y install kernel-devel-$(uname -r)
    ```

3. Install Falco:

    ```shell
    yum -y install falco
    ```
    Falco, the kernel module driver, and a default configuration are now installed. 
    Falco is being ran as a systemd unit.   
    
    See [running](../running) for information on how to manage, run, and debug with Falco. 


4. Uninstall Falco:

    ```shell
    yum erase falco
    ```
