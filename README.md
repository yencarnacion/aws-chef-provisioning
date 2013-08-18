# aws-chef-docker 

## Description

Installs Chef and Docker using the Vagrant AWS Provider.  Builds on https://github.com/bflad/chef-docker and https://github.com/mitchellh/vagrant-aws 

## Usage

Install using standard Vagrant 1.1+ plugin installation methods. After
installing, `vagrant up` and specify the `aws` provider. An example is
shown below.

```
$ vagrant plugin install vagrant-aws 
```

```
$ vagrant up --provider=aws
```

