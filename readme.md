# XRootD Monitor

## Description

A XRootD setup using different XCache proxies via the http and xrootd protocols

## dependencies

Manages hostfiles via [vagrant-hosts](https://github.com/oscar-stack/vagrant-hosts)
Install via:
```
vagrant plugin install vagrant-hosts
```

## Setup

Up and provision the setuo
```
vagrant up
```

## Test setup

Access the client using vagrant ssh and test the different XCache proxies 

```
vagrant ssh client
xrdcp -f xroot://server//100M .
xrdcp -f xroot://proxy//100M .
xrdcp -f xroot://memoryproxy//100M .
xrdcp -f xroot://diskproxy//100M .
curl -O http://server:1094/10M
curl -O http://proxy:1094/10M
curl -O http://memoryproxy:1094/10M
curl -O http://diskproxy:1094/10M
```

