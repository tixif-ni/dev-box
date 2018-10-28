# Dev box

## Requirements
* [Vagrant](https://www.vagrantup.com) version 2.2+ available
* [Vagrant disk size](https://github.com/sprotheroe/vagrant-disksize)
* [Vagrant host manager](https://github.com/devopsgroup-io/vagrant-hostmanager)
* [Vagrant hosts](https://github.com/oscar-stack/vagrant-hosts)
* `shared_folder` sibling to where the project has been cloned to sync files

## Start

All commands default to the master box when not specified. To get started
simply run:
```sh
> vagrant up [box]
```

If any updates occurs to the provisioning scripts run
```sh
> vagrant provision [box]
```

## Login

Enter any of the boxes via
```sh
> vagrant ssh [box]
```
