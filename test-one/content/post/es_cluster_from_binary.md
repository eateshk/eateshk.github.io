---
title = "Elastic Search Cluster Setup from Binary"
date = "2018-11-26"
Xdescription = "On Ubuntu on Azure"
---

# Preparation 

## Step 1
Get an ubuntu box - you can find  [version compatibility](https://www.elastic.co/support/matrix)

### On Azure
    Using ubuntu 16.04 LTS
    1) Create a machine with public ip(master node)
    2) Create other machines (data/ingest nodes w/o public IP)


## Step 2
Install Oracle Java. Compatibility matrix in same link as above.
> sudo apt-get update && sudo apt-get upgrade
> sudo apt-get install software-properties-common
> sudo add-apt-repository ppa:linuxuprising/java
> sudo apt-get update
> sudo add-apt-repository ppa:webupd8team/java
> sudo apt-get update
> sudo apt-get install oracle-java8-installer

Set JAVA_HOME
> vim /etc/environment 
>   Add below content
>   > JAVA_HOME="/usr/lib/jvm/java-8-oracle"
>   > export JAVA_HOME
> source /etc/environment

## Step 3
wget <path to debian binary>
Example -  
> wget https://download.elastic.co/elasticsearch/release/org/elasticsearch/distribution/deb/elasticsearch/2.4.1/elasticsearch-2.4.1.deb.sha1
> sudo dpkg -i elasticsearch-2.4.1.deb

## Step 4
Configurations file => /etc/elasticsearch/elasticsearch.yml
Need to set these configurations differently on different machines according to what's needed {master nodes, data nodes, ingestion nodes}
> cluster.name: es.cluster
> // keep cluster name same for everything in the cluster
> node.name: node-1
> // keep node names different but recognizable
> node.data: true
> node.master: false
> network.host: [10.0.0.7, _local_]
> // this should contain node itself _local_ is for loopback, IP is ip address in the cluster vpn.
> discovery.zen.ping.unicast.hosts: ["10.0.0.7", "10.0.0.6"]
>  // this should contain the links to all the nodes (It may contain less then all too though. Should include itself ?)


## Step 5 Start/Stop Service
>  sudo /bin/systemctl daemon-reload
>  sudo /bin/systemctl enable elasticsearch.service
>  sudo systemctl start elasticsearch.service

## Check Health
http://master_ip:port/_cluster/stats?human&pretty






