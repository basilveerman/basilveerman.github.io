---
layout: post
title: Installing Ubuntu on a Dell XPS 13 9350
---

### Get the latest kernel

```bash
mkdir kernel45
cd kernel45
wget http://kernel.ubuntu.com/~kernel-ppa/mainline/v4.5-wily/linux-headers-4.5.0-040500_4.5.0-040500.201603140130_all.deb
wget http://kernel.ubuntu.com/~kernel-ppa/mainline/v4.5-wily/linux-headers-4.5.0-040500-generic_4.5.0-040500.201603140130_amd64.deb
wget http://kernel.ubuntu.com/~kernel-ppa/mainline/v4.5-wily/linux-image-4.5.0-040500-generic_4.5.0-040500.201603140130_amd64.deb
```

Install them and reboot

```bash
sudo dpkg -i linux-headers-4.5*.deb linux-image-4.5*.deb
sudo reboot
```

### Wireless:

```bash
wget http://en.community.dell.com/cfs-file/__key/telligent-evolution-components-attachments/00-4613-01-00-20-84-05-08/brcmfmac4350_2D00_pcie.zip
unzip brcmfmac4350_2D00_pcie.zip
sudo mv brcmfmac4350-pcie.bin /lib/firmware/brcm/
sudo chmod 600 /lib/firmware/brcm/brcmfmac4350-pcie.bin
```

[source](http://www.ambience.sk/dell-xps13-touch-9350-ubuntu-black-screen-boot-wifi/)


### VPN

```bash
sudo apt-get install network-manager-openconnect
```

### Power management

```bash
sudo apt-get install tlp tlp-rdw smartmontools ethtool
sudo tlp start
```

Configure as per [the docs](http://linrunner.de/en/tlp/docs/tlp-configuration.html).

Also, check out [Ubuntu power saving tweaks](https://wiki.ubuntu.com/Kernel/PowerManagement/PowerSavingTweaks)


