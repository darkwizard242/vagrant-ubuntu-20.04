[![Build Status](https://travis-ci.com/darkwizard242/vagrant-ubuntu-20.04.svg?branch=master)](https://travis-ci.com/darkwizard242/vagrant-ubuntu-20.04)

# 1\. ubuntu2004

`ubuntu2004` is a Vagrant VM box built using [Packer](https://www.packer.io/), [Vagrant](https://www.vagrantup.com/) and [VirtualBox](https://www.virtualbox.org/). It uses **Official Ubuntu 20.04 LTS server iso** as the underlying image.

`ubuntu2004 Releases`: [Vagrant Cloud URL](https://app.vagrantup.com/darkwizard242/boxes/ubuntu2004)

Supported Provider: **VirtualBox**

## Audience

IT professionals, organizations, enthusiasts or learners who wish to utilize an Ubuntu 20.04 LTS vagrant box built using Official Server Image.

## Disclaimer:

It is expected that you have Vagrant and Virtualbox installed on your host machine (whether the host is Windows, Linux or OSX). If not, then please download/install [Vagrant](https://www.vagrantup.com/downloads.html) and [Virtualbox](https://www.virtualbox.org/wiki/Downloads).

# 2\. Virtualizing `ubuntu2004` on Vagrant

This section covers easy to use steps to get started with downloading and virtualizing `ubuntu2004` virtual environment.

## 2.1\. Single Machine Mode:

Single Machine mode is a mode where you will only be initializing a fresh vagrant virtual envrionment to use`ubuntu2004`. Open CMD (for **Windows** host) or Terminal (for **Linux/OSX** host), then change to a directory of your liking on the Command Prompt or Terminal and run the following command:

```shell
vagrant init darkwizard242/ubuntu2004
```

Now that `Vagrantfile` has been created for `ubuntu2004`, you can initialize/boot up the box (it will download the box if not already downloaded) using the following command:

```shell
vagrant up
```

Once the box is up, do `vagrant ssh` and you will be within the virtualized box.

## 2.2\. Multi Machine Mode:

As per Vagrant's website, "Vagrant is able to define and control multiple guest machines per Vagrantfile. This is known as a 'multi-machine' environment." So if you are running in a **multi-machine mode**, you can simple add the following chunk within the existing Vagrantfile:

```shell
config.vm.define "myubuntubox" do |myubuntubox|
   myubuntubox.vm.box = "darkwizard242/ubuntu2004"
   myubuntubox.vm.hostname = 'focalfossa.ubuntu.com'
end
```

Now run the following command so that the box can be downloaded (if not already) and be booted up:

```shell
vagrant up mydevopsbox
```

Once the box is up, do `vagrant ssh mydevopsbox` and you will be within the virtualized box.

# 3\. Users - for `ubuntu2004` Vagrant box

Like any other vagrant box, you can easily ssh into ubuntu2004 using the default `vagrant ssh` (if using as a single machine mode) command or `vagrant ssh myubuntubox` if using in a multi machine mode.

## 3.1\. Type and list of users and passwords:

Below is table listing the type of users as well as their usernames and passwords:

User Type   | Username | Password
----------- | -------- | --------
System User | vagrant  | password

**NOTE:** _Though, the password for vagrant user has been set by default by me so that anyone can use it easily. Feel free to change the password using the following command:_

- `passwd vagrant`

## 3.2\. Users and permissions:

Following users have already been added as **sudoers** with privileges to perform desired operations without supplying passwords:

```shell
root@ubuntu2004:~$ grep -i vagrant /etc/sudoers
vagrant ALL=(ALL) NOPASSWD: ALL
```

## 3.3\. Users and home directories:

Following table consists the system **users** and their `$HOME` directories.

User    | Home Directory
:------ | :-------------
root    | /root
vagrant | /home/vagrant

# 4\. `ubuntu2004` Build & Testing:

Vagrant box `ubuntu2004` can be built using Packer. Pre-requisites include Virtualbox as that is the builder being used for the packer build.

## 4.1\. Building out your own customized `ubuntu2004`:

Assuming that Virtualbox and Packer are installed on the host system with internet accessibility, you can build `ubuntu2004` yourself using the following steps:

1. Downloading **ubuntu2004** source code archive: `wget -O vagrant-ubuntu-20.04.zip https://github.com/darkwizard242/vagrant-ubuntu-20.04/archive/master.zip`
2. Extracting **vagrant-ubuntu-20.04** source code archive: `unzip vagrant-ubuntu-20.04.zip -d .`
3. Changing to packer build directory: `cd vagrant-ubuntu-20.04-master`
4. Once customized, run a packer build using: `packer build template-branch-others.json`

# 4.2\. Initializing your customized version of `ubuntu2004` Build:

Once you have built out a `ubuntu2004` box. You can easily test it out by adding it as vagrant box using the following commands:

1. `vagrant box add myubuntubox` /path/to/ubuntu2004.box - This command will add the newly built customized ubuntu2004 box to vagrant so that it can be used. It would be wise to use the exact path to the ubuntu2004 box you have built.

2. `vagrant init myubuntubox` - This command will initialize the box you have associated your vagrant image with.

3. `vagrant up myubuntubox` - Boots up the box.

# Acknowledgements:

- [Packer](https://www.packer.io/)
- [Vagrant](https://www.vagrantup.com/)
- [Ubuntu](https://www.ubuntu.com/)
- [VirtualBox](https://www.virtualbox.org)

# Authors:

- [Ali Muhammad](https://www.linkedin.com/in/ali-muhammad-759791130/)
