# ansible-couchdb2
Ansible role to deploy CouchDB 2.0 on CentOS.

This repo contains an Ansible role to install CouchDB 2.0 on CentOS 6.7 machines. It's been tested with Ansible 1.9.4.

The role roughly follows the instructions from the CouchDB 2.0 Release Testing Plan (see https://docs.google.com/document/d/1BtndYr-0KDQTqBSLVdJoR_8C5ObYjT1RBo_Qyh5ykdQ/edit#)

The role is fairly self explanatory. It installs SpiderMonkey, Erlang, Node.js and then proceeds to build CouchDB 2.0 from the Github sources. 

The process take a little while, but at the end, you have a running CouchDB 2.0 installed as a Linux service (via a sysv script). 
