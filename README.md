# k3os_vagrant_libvirt

Most of this was taken from the official [k3os repository](https://github.com/rancher/k3os/tree/master/package/packer/vagrant) and adapted to work with libvirt.

## Quick Start

1. Build the vagrant box using [Packer](https://www.packer.io/):

```bash
# JSON syntax
packer build template.json
# HCL syntax
packer build template.pkr.hcl
```

2. Import the vagrant box

```bash
vagrant box add --provider libvirt k3os k3os_libvirt.box
```

3. Make sure the permissions on the `packer_rsa` file are strict enough:
```bash
chmod 400 packer_rsa
```

4. Run the vagrant box:

```bash
vagrant up
```

You can then login to the box using `vagrant ssh`. See [Vagrant
Docs](https://www.vagrantup.com/docs/index.html) for more details on how
to use Vagrant
