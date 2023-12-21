# kubernetes-guide #

## Scope of application ##

Mostly this guidance is for the user who **don't have any experience** in kubernetes deployment on debian(linux) system 
## Environment ## 


Debian 12.4 (up-to-date to latest at 2023/12/20)
containerd
Kubernetes v1.29.0 (up-to-date at 2023/12/21)


## Content ##

If you are a experienced linux user , can skip to step .

### Background ###

There is one thing have to discuss with, In Debian 12.4 the text editor -- nano is easy to use for the **beginners**.(Just a recommend)
It is also allowed to use other text editor like -- vi/vim.

### Step 1 obtain the sys access authority ###

After start the Debian System you will see the image as below.

![image](./image-upload/1.jpg)

#### Alternative ####
    su -
The system will ask you for the root password.

##### For Learning Environment #####

Skip to next step

##### For Poduction Environment  #####

    nano /etc/sudoers
![image](./image-upload/2.jpg)
Locate at the line as below:

    # Allow members of group sudo to execute any command
    %sudo   ALL=(ALL:ALL) ALL

Then add your system account below to obtain the system access authority.
(**This is based on your production environment system-access structure**. )

Here offers the full-access to the example account.

`dawnliving ALL=(ALL:ALL) ALL`

![image](./image-upload/3.jpg)

(For the `nano` text editor press `Ctrl+O` and `Enter` to save the change to the file and press `Ctrl+X` to exit)

(For the `vi/vim` usually to press `:` ,  then input `wq` then press `Enter` to save and exit)

### Step 2 Edit the Package Repository ###

This step mainly talked about how to edit apt repository. There have a lot of ways to install required apps and kubernetes. But in this guidance, all the required apps and kubernetes(k8s) will be installed by **apt** package control tool(**Debian/Ubuntu**, in Centos uses yum).

`nano /etc/apt/source.list`

Then visit the website(Here offer the official repository example)

[https://wiki.debian.org/SourcesList](https://wiki.debian.org/SourcesList)

In this website, need to find the example that official offers, then find the exact version of the operating system.
(This guide will choose Debian 12(Bookworm).)

The example as below:

![image](./image-upload/4.jpg)

Then paste one example(based on your requirement) to `source.list` save and exit.

### Step 3 Proxy Setting (If needed) ###

**Notice**: 

1. If your environment need to connect the Internet by Proxy. The guidance as below.
2. This step is **not necessary** for all users. If needed, continue reading. If not, skip to next step.

The root system access authority is needed. If the user log in is not root, the `sudo` is needed to attach to the front of all the following commands.

`systemctl set-environment http_proxy=your-example:port`

`systemctl set-environment https_proxy=your-example:port`

`systemctl set-environment no_proxy=localhost,127.0.0.0/8,192.168.0.0/16,10.0.0.0/8,172.16.0.0/12`

Setting as above will let the system all the Internet connection through the proxy setting except the `no_proxy` declaration. If you don't want other service that don't mention in the guidance connect to the Internet through the proxy, modify the `no_proxy` setting, in case lead to other service connection refused error.

### Step 4 Container Runtimes Installation###
To be continued.