targetd
=======

Remote configuration of a LIO-based storage appliance
-----------------------------------------------------
targetd turns Linux into a remotely-configurable storage appliance. It
supports an HTTP/jsonrpc-2.0 interface to let a remote administrator
allocate volumes from an LVM volume group, and export those volumes
over iSCSI.  It also has the ability to create remote file systems and export
those file systems via NFS/CIFS (work in progress).

targetd development
-------------------
targetd is licensed under the GPLv3. Contributions are welcome.
 
 * Mailing list: [targetd-devel](https://lists.fedorahosted.org/mailman/listinfo/targetd-devel)
 * Source repo: [GitHub](https://github.com/agrover/targetd)
 * Bugs: [GitHub](https://github.com/agrover/targetd/issues) or [Trac](https://fedorahosted.org/targetd/)
 * Tarballs: [fedorahosted](https://fedorahosted.org/releases/t/a/targetd/)

**NOTE: targetd is STORAGE-RELATED software, and may be used to
  remove volumes and file systems without warning from the resources it is
  configured to use. Please take care in its use.**

Getting Started
---------------
targetd has these Python library dependencies:
* [targetcli] (https://github.com/agrover/targetcli-fb) (must be fb*)
* [python-rtslib](https://github.com/agrover/rtslib-fb) 2.1.fb14+  (must be fb*)
* [python-lvm](https://github.com/agrover/python-lvm) 1.2.2+
* [python-setproctitle](https://github.com/dvarrazzo/py-setproctitle)
* [PyYAML](http://pyyaml.org/)

All of these are available in Fedora Rawhide.

### Configuring targetd

A configuration file may be placed at `/etc/target/targetd.yaml`, and
is in [YAML](http://www.yaml.org/spec/1.2/spec.html) format. Here's
an example:

    user: "foo" # strings quoted, or not
    password: bar
    ssl: false
    target_name: iqn.2003-01.org.example.mach1:1234

    block_pools: [vg-targetd, vg-targetd-too]
    fs_pools: [/mnt/btrfs]

targetd defaults to using the "vg-targetd" volume group, and username 'admin'.
The admin password does not have a default -- each installation must set it.

Then, run `sudo ./targetd.py`.

client.py is a basic testing script, to get started making API calls.
