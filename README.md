# ansible-couchdb2
An Ansible role to deploy a CouchDB 2.0 release candidate on CentOS 6.x

## Overview
This repo contains an Ansible role to install CouchDB 2.0 on CentOS 6.x machines. It's been tested with Ansible 1.9.4 and CentOS 6.7/6/8.

The role roughly follows the instructions from the CouchDB 2.0 Release Testing Plan (see https://docs.google.com/document/d/1BtndYr-0KDQTqBSLVdJoR_8C5ObYjT1RBo_Qyh5ykdQ/edit#)

## In the box
The role is fairly self explanatory. It installs SpiderMonkey, Erlang (from Erlang Solutions), Node.js 4.x and then proceeds to build CouchDB 2.0 from the Github sources.

The process may take a little while, but at the end, you will have a running CouchDB 2.0 installed as a Linux service (via a sysv script).

## Build a given release candidate

By default, the role builds the latest release candidate (as of 05/09/2016, that is RC4). You can also specify another RC version when deploying the role via the release_candidate variable, like so:

`ansible-playbook -i inventory -e "release_candidate=RC3" couchdb2.yaml`

For a list of available RCs, please see: https://couchdb.apache.org/release-candidate/2.0/

## Cluster setup

If you deploy on multiple nodes at once, you can also use the role to configure those nodes in a cluster, simply set the variable configure_cluster to True (by default it is set to False).

The role will then connect all the machines which are in the couches inventory group as per the steps described in https://github.com/apache/couchdb-setup (the instructions on that page are not 100% correct, some of the URLs have typos in them).

This can be done in your inventory file, or via a command-line parameter, like so :

`ansible-playbook -i inventory -e "configure_cluster=True" couchdb2.yaml`

In Cluster mode, the role automatically creates an admin account (user: admin, password: password). 

## Warning

At present, the playbook disables the firewall, so use at your own risk. I am working on an updated version which uses Ansible to poke the correct holes in IPTables.

