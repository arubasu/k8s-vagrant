# k8s-vagrant
Create a local kubernetes cluster using virtualbox and monitoring with Prometheus<br>
### Credits:
  [danielepolencic](https://github.com/danielepolencic) -> [gist](https://gist.github.com/danielepolencic/ef4ddb763fd9a18bf2f1eaaa2e337544)<br>
  https://github.com/LocusInnovations/k8s-vagrant-virtualbox


The vagrant file will do the following:
---------------------------------------
1.  Provision all local VMs using VirtualBox with Port forwarding to access Prometheus(30090), Alert Manager(30093) and Grafana(30000)
2.  Patch the OS
3.  Install Docker
4.  Install k8s control plane
5.  Initialize cluster with Flannel CIDR block & install Flannel
6.  Join the nodes to the master
7.  Create and copy the SSH key to all machines so you can SSH to any node from the Master.  Add names & IPs to the local hosts file on each master and node.
8.  Make required Ubuntu OS mods for the cluster to function properly

## Dependencies

You should install [VirtualBox](https://www.virtualbox.org/wiki/Downloads) and [Vagrant](https://www.vagrantup.com/downloads.html) before you start.

Open a shell and install the vagrant disksize plugin:
```bash
$ vagrant plugin install vagrant-disksize
```

## Make sure git is installed

Instal [git](https://git-scm.com/downloads) if you don't already have it.

## Open a shell and clone

```bash
$ git clone https://github.com/arubasu/k8s-vagrant.git
$ cd k8s-vagrant
```

## Starting the cluster

You can create the cluster with:

```bash
$ vagrant up
```

## Clean up

You can delete the cluster with:

```bash
$ vagrant destroy -f
```

## SSH and other Commands

SSH to Master and other Nodes:

```bash
$ vagrant ssh master
$ vagrant ssh node1
$ vagrant ssh node2
$ vagrant ssh node3
```

Get the status of the Nodes:

```bash
root@master:/home/vagrant# kubectl get nodes -o wide
NAME     STATUS   ROLES                  AGE     VERSION   INTERNAL-IP   EXTERNAL-IP   OS-IMAGE             KERNEL-VERSION       CONTAINER-RUNTIME
master   Ready    control-plane,master   2d21h   v1.21.1   10.0.0.10     <none>        Ubuntu 18.04.5 LTS   4.15.0-143-generic   docker://20.10.2
node1    Ready    <none>                 2d21h   v1.21.1   10.0.0.11     <none>        Ubuntu 18.04.5 LTS   4.15.0-143-generic   docker://20.10.2
node2    Ready    <none>                 2d21h   v1.21.1   10.0.0.12     <none>        Ubuntu 18.04.5 LTS   4.15.0-143-generic   docker://20.10.2
node3    Ready    <none>                 2d21h   v1.21.1   10.0.0.13     <none>        Ubuntu 18.04.5 LTS   4.15.0-143-generic   docker://20.10.2
root@master:/home/vagrant#
```

SSH to other Nodes in the cluster from the Master `vagrant ssh master`:

```bash
$ ssh node1
$ ssh node2
$ ssh node3
```

### Follow the link for installting Prometheus setup for this k8s cluster.
https://github.com/arubasu/k8s-prometheus
