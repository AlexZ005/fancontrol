# Fancontrol Script (Debian Packaging)

This repository provides a simple script to control fan speed based on temperature, packaged for Debian/Ubuntu systems.

---

## Building the .deb Package

### 1. Prepare the source tarball

Debian expects an upstream source tarball named `<package>_<version>.orig.tar.gz`. From current directory run:

```bash
tar czf ../fancontrol_0.1.orig.tar.gz ./
```

### 2. Build .deb package

```bash
debuild -us -uc
```

### 2.1 Optional: Repack .deb package

gzip can be used if dpkg on router is outdated and following error appears:
```
Error:
dpkg-deb: error: archive './fancontrol_0.1-1_all.deb' uses unknown compression for member 'control.tar.zst', giving up
```

```bash
dpkg-deb -R ../fancontrol_0.1-1_all.deb /tmp/fancontrol_0.1-1_all.deb
dpkg-deb -Zgzip -b /tmp/fancontrol_0.1-1_all.deb fancontrol_0.1-1_all_gzip.deb
```
### 3. Install the package

```bash
sudo dpkg -i ./fancontrol_0.1-1_all.deb
```

### 4. Update config and reload service

To configure fan min/max speed edit /etc/fancontrol.conf

```bash
systemctl restart fancontrol.service
systemctl status fancontrol.service
```
---

## Disclaimer ⚠️
This program is provided **as is**, without any warranty.  
Using it may affect your hardware. **You use it at your own risk.**  
The author is not responsible for any possible damage.

---