# Install-kubernetes-kubeadm

![Visits Badge](https://badges.pufler.dev/visits/mrunix1998/docker-minio-cluster)
![GitHub last commit](https://img.shields.io/github/last-commit/mrunix1998/docker-minio-cluster)
[![GitHub issues](https://img.shields.io/github/issues/mrunix1998/docker-minio-cluster)](https://github.com/mrunix1998/docker-minio-cluster/issues)
[![GitHub stars](https://img.shields.io/github/stars/mrunix1998/docker-minio-cluster)](https://github.com/mrunix1998/docker-minio-cluster/stargazers)
[![GitHub forks](https://img.shields.io/github/forks/mrunix1998/docker-minio-cluster)](https://github.com/mrunix1998/docker-minio-cluster/network)

[![Gmail](https://img.shields.io/badge/Gmail-D14836?style=for-the-badge&logo=gmail&logoColor=white)](salehimohammad331@gmail.com)
![Ansible](https://img.shields.io/badge/ansible-%231A1918.svg?style=for-the-badge&logo=ansible&logoColor=white)
<a href="https://www.linkedin.com/in/mrunix1998/" style="text-align:center">
  <img
    alt="Linkedin"
    src="https://img.shields.io/badge/linkedin-0077B5?logo=linkedin&logoColor=white&style=for-the-badge"
  />
</a>

## Create python virtual environment

First install package in python :

```bash
$ apt install python3.8-venv
```

Then create new environment :

```bash
$ python3 -m venv venv
```

Finally activate your environments :

```bash
$ source venv/bin/activate
```

## Install requirements packages

First upgrade your pip to latest version :

```bash
$ pip install --upgrade pip
```

For installing requirements run below commands :

```bash
$ pip install -r requirement.txt
```

#
## Create Cluster

### Modifying hosts file

For joining masters and workers nodes to ansible's hosts changing hosts file :

```bash
$ vim hosts
```

### Create ssh key and send to all nodes

For connecting ansible user to all nodes and running roles in them, run the following commands :

```bash
# ssh-keygen
```

```bash
vim /etc/hosts
```

```code
192.168.119.104 master
192.168.119.107 worker1
192.168.119.223 worker2
192.168.119.123 worker3
```

**Note :** According to your workspace you should change your masters and workers node ips


```bash
# ssh-copy-id root@master1
# ssh-copy-id root@master2
# ssh-copy-id root@master3
.
. . .
.
# ssh-copy-id root@worker1
# ssh-copy-id root@worker2
# ssh-copy-id root@worker3
```

### Testing ansible

For testing that ansible connected to all your nodes run below command :

```bash
$ ansible -i hosts all -m ping
```


### Initiate kubernetes user

Creating kubernetes user for cluster with following command :

```bash
$ ansible-playbook -i hosts users.yml
```

### Install docker on all nodes

For friendly work with kubernetes running cluster with docker interface

```bash
$ ansible-playbook -i hosts docker.yml
```

📌 **Note :** After you add kubernetes user and installed docker you should run the following command :

```bash
# usermod -aG docker <kubernetes_user>
```

### Install kubernetes

Installing kubernetes packages for initiate cluster :

```bash
$ ansible-playbook -i hosts install-k8s.yml
```

### Creating a Kubernetes Cluster Master Node

Join first node as master node with following command :

```bash
$ ansible-playbook -i hosts master.yml
```

### Join Worker Nodes to Kubernetes Cluster

Join nodes as workers run the following command :

```bash
$ ansible-playbook -i hosts join-workers.yml
```