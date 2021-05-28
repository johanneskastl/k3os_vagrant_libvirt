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

In case you want to start again, remove the box from vagrant and start again with step1.
```bash
vagrant box remove k3os
```
## Fetching the kubeconfig file using Ansible

In case you have Ansible installed, uncomment the provision block in the Vagrantfile before running `vagrant up`, and this will fetch the kubeconfig file to the local machine named as `k3os-kubeconfig`. You can then connect to your kubernetes cluster using `kubectl --kubeconfig k3os-kubeconfig get nodes` or similar.

You can also run this after the `vagrant up` step by issuing `vagrant provision`.

To make this work, you need to make sure the roles/fetch_k3os_kubeconfig git submodule is fully available:
```
git submodule init roles/fetch_k3os_kubeconfig/
git submodule update roles/fetch_k3os_kubeconfig/
```
