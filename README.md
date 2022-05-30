# Kubernetes the IaC Way


## Introduction

**kubernetes-the-iac-way** is a challenge I set myself after completing [Mumshad](https://github.com/mmumshad)'s version of [kubernetes-the-hard-way](https://github.com/mmumshad/kubernetes-the-hard-way).

The goal is to deploy "Kubernetes The Hard Way" in one command using Infrastructure as Code (IaC).

The project is based on Vagrant for the creation of nodes (Vagrantfile), and Ansible for the installation of Kubernetes in each node created (playbook.yml).

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


## In the future

Currently, the project allows to install Kubernetes on **two master nodes**, **two worker nodes** and **one load balancer node**; in the *192.168.42.0/24* subnet.

In the future, the code will allow to generate as many nodes as desired in any subnet by editing the Vagrantfile.
