Ansible Linux
=============

Various ansible scripts I use to setup my home systems. Based on
the [Arch Linux Installation Guide](https://wiki.archlinux.org/title/installation_guide)

## Prerequisites

Install a ansible into a virtual environment

```
python -m venv venv
source venv/bin/activate
pip install -r requirements.txt
```

Create a variables file called `vars.yml` (see `vars.example.yml`) for an example
for private data. This will not be checked into the repository

Edit the IP address of `system` in `inventory`

## Preinstallation

Runs the [Preinstallation](https://wiki.archlinux.org/title/installation_guide#Pre-installation)
steps as far as and including mounting the filesystems

```
$ ansible-playbook -K arch_preinstall.yml --extra-vars "@vars.yml"
```

Before continuing, verify that the encryption password is correctly set with
```
$ cryptsetup open --test-passphrase <passphrase>
```

## Chroot and Configuration

Run the installation steps after [chroot'ing](https://wiki.archlinux.org/title/installation_guide#Chroot)
into the system. This needs to be run locally on the target system

```
ansible-playbook -K arch_chroot_install.yml --extra-vars "@vars.yml"
```

## Post Installation

Run the main post installation steps

```
ansible-playbook -K site.yml --extra-vars "@vars.yml"
```

To run a particular role, use the corresponding tag, for example

```
ansible-playbook -K site.yml -t developer
```
