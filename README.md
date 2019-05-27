# esdeploy

### ESdeploy is a tool to quickly deploy an Elastic Stack for testing and demonstration purposes

ESdeploy is a collection of modified Ansible recipies when used along with Vagrant allow any user to locally create and tear down various components of the Elastic Stack locally, all using local virtual machines which provide complete isolation from one another and from your machine.

This means that you can easily use ESdeploy to create an environment for testing or for demonstration and even recreate that environment the same way as many times as you like!

### Installation

To use ESdeploy, just clone the repo onto your workstation. ESdeploy has the following prerequsites:

* Ansible
* Vagrant

To install the necessary software on OS X, the following commands will suffice:

```
brew cask install virtualbox
brew cask install vagrant
brew install ansible
```

### Usage

Use Vagrant directly to bring machines up and down. For example, to bring up an Elasticsearch node along with a Kibana instance, type the following from the `esdeploy` installation directory:

`vagrant up es1.prod kb1.prod`

After doing so, ESdeploy will bring up two machines, both with Ubuntu base images. You can access Kibana via your browser at http://localhost:5601. (Note that you should not have either an Elasticsearch or a Kibana instance running locally as of this version of ESdeploy. This will be rectified in later versions.)

To access either the Elasticsearch or the Kibana hosts directly via SSH, use `vagrant ssh`. For example, to get dropped into a shell prompt on the Kibana machine, type:

`vagrant ssh kb1.prod`

To reset a machine to a known-good state, any machine can be immediatley reprovisioned without needing to reboot it. For example, to reset the Kibana instance to a known-good state, type:

`vagrant up kb1.prod --provision`

To completely destroy and reset a machine, use the `destroy` command followed by the `up` command. For example, to redeploy the Elasticsearch node, type:

`vagrant destroy es1.prod && vagrant up es1.prod`

### Stack Availability

Presently, the following Stack components are available:

* Elasticsearch
* Kibana
* Logstash

### Contributions

Contributions are welcome!
