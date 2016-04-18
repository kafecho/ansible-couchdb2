# ansible-couchdb2
An Ansible role to deploy CouchDB 2.0 on CentOS 6.7.

## Overview
This repo contains an Ansible role to install CouchDB 2.0 on CentOS 6.7 machines. It's been tested with Ansible 1.9.4.

The role roughly follows the instructions from the CouchDB 2.0 Release Testing Plan (see https://docs.google.com/document/d/1BtndYr-0KDQTqBSLVdJoR_8C5ObYjT1RBo_Qyh5ykdQ/edit#)

## In the box
The role is fairly self explanatory. It installs SpiderMonkey, Erlang, Node.js and then proceeds to build CouchDB 2.0 from the Github sources.

The process takes a little while (CouchDB fetches quite a few Git repos), but at the end, you have a running CouchDB 2.0 installed as a Linux service (via a sysv script).

## Build a given git version

By default, the role builds the latest (HEAD) git version. You can also specify another version when deploying the role via the git_version variable, like so:

`ansible-playbook -i inventory -e "git_version=a18004d43cdc6924ce6e43a59d058e4cba5b91a1" couchdb2.yaml`

## Cluster setup

If you deploy on multiple nodes at once, you can also use the role to configure those nodes in a cluster, simply set the variable configure_cluster to true (by default it is set to false).

The role will then connect all the machines which are in the couches inventory group as per the steps described in https://github.com/apache/couchdb-setup (the instructions on that page are not 100% correct, some of the URLs have typos in them).

This can be done in your inventory file, or via a command-line parameter, like so :

`ansible-playbook -i inventory -e "configure_cluster=true" couchdb2.yaml`

## Warning

At present, the playbook disables the firewall, so use at your own risk. I am working on an updated version which uses Ansible to poke the correct holes in IPTables.

