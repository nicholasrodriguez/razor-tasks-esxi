# Ansible Role: Razor Tasks ESXi

An Ansible Role that configures Tasks and Repos in Puppet Razor on Linux.

## Razor Summary

PuppetLabs Razor Server is an Open Source Operating System provisioning tool, details are here:

[https://github.com/puppetlabs/razor-server/wiki]

## Razor Post Task Configuration Use

This role will only create custom ESXi Tasks and Repos in Razor. As kickstart files are tailored to the environment you are deploying to the intention is this Role will be cloned and the kickstart files can be altered as per your environment. Hopefully they help.

I've created the following personal Ansible Role for creating Razor Policies and Tags which inject the metadata variables into the kickstarts e.g. ```<%= node.metadata['mgmt_nic'] %>```:

* nicholasrodriguez.razor_manage_hosts (IN DEV)

These can be copied and used as template for your own environments.

# Requirements

This Role was built and tested after the following Role was deployed but could be used for other Razor deployments not managed by the Role below:

* nicholasrodriguez.razor

The ESXi ISO/s need to be hosted on an accessible web file share from the Razor server.

# Role Variables

Available variables are listed below, along with default values (see defaults/main.yml):

ESXi version/s to install. A list of dicts specifying the following, examples are below and at least one entry is required.
```
esxi_versions:
  - major: "MAJOR RELEASE NUMBER"
    build: "ESXi-BUILDNUMBER"
    url: "http://address/path/VMware-VMvisor-Installer-VERSION.iso"
```

Example
```
- major: "6.7"
  build: "ESXi-6.7.0-15160138"
  url: "http://address/path/VMware-VMvisor-Installer-201912001-15160138.x86_64.iso"
```

ESXi boot.cfg kernel parameters, only set this to true in non-production environments as it enables non-supported CPUs.
```
allowLegacyCPU: false
```

# Example Playbook
```
- hosts: servers
  roles:
     - role: nicholasrodriguez.razor-tasks-esxi
```

License
-------

MIT

Author Information
------------------

- https://github.com/nicholasrodriguez/ (maintainer)
