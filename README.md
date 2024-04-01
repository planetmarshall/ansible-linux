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

## Preinstallation

Runs the [Preinstallation](https://wiki.archlinux.org/title/installation_guide#Pre-installation)
steps as far as and including mounting the filesystems

```
ansible-playbook -K arch_preinstall
```

## Chroot and Configuration

Run the installation steps after [chroot'ing](https://wiki.archlinux.org/title/installation_guide#Chroot)
into the system

```
ansible-playbook -K arch_chroot_install
```

## Post Installation

Run the main post installation steps

```
ansible-playbook -K site.yml
```

To run a particular role, use the corresponding tag, for example

```
ansible-playbook -K site.yml -t developer
```
