# Kubernetes the IaC Way


## Technologies used

![Kubernetes](https://img.shields.io/badge/kubernetes-%23326ce5.svg?style=for-the-badge&logo=kubernetes&logoColor=white)
![Ansible](https://img.shields.io/badge/ansible-%231A1918.svg?style=for-the-badge&logo=ansible&logoColor=white)
![Vagrant](https://img.shields.io/badge/vagrant-%231563FF.svg?style=for-the-badge&logo=vagrant&logoColor=white)


## Introduction

**kubernetes-the-iac-way** is a challenge I set myself after completing [Mumshad](https://github.com/mmumshad)'s version of [kubernetes-the-hard-way](https://github.com/mmumshad/kubernetes-the-hard-way).

The goal is to deploy "Kubernetes The Hard Way" in **one command** using Infrastructure as Code (IaC).

The project is based on Vagrant for the creation of nodes (Vagrantfile), and Ansible for the installation of Kubernetes in each node created (playbook.yml). It takes only **10 minutes** to deploy.

Before using this repository, I strongly recommend that those who have never deployed "[Kubernetes The Hard Way](https://github.com/mmumshad/kubernetes-the-hard-way)" give it a try to better understand how Kubernetes works.


## How it works

Clone the repository, then run the `vagrant up` command.

By doing so, Vagrant will take care of creating the nodes via the Vagrantfile, then launch the Ansible playbook on each node during their creation.


## Prerequisites

### Hardware requirements

RAM: 8 GB minimum | 16 GB recommended

Disk space: 50 GB


### Software requirements

Install [Vagrant](https://www.vagrantup.com/downloads) & [Ansible](https://docs.ansible.com/ansible/latest/installation_guide/intro_installation.html)


## Modify the configuration

By default, the project allows to install Kubernetes on **three master nodes**, **two worker nodes** and **one load balancer node**; in the *192.168.42.0/24* subnet.

You can generate as many master and worker nodes as desired in any subnet by editing the variables at the beginning of the Vagrantfile.
