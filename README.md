# Platform

## Overview

There's a wealth of information available about technology platforms, primarily operating systems, hypervisors, and various computer architectures. There are also endless debates of which ones are the "best".  One of the biggest challenges when supporting, say, multiple operating systems on multiple architectures running on physical, virtualized, and containerized environments is establishing build and testing infrastructure for CI/CD and implementing processes to maintain them.  

The purpose of this repository is to codify information of platforms, that we can use in turn to automate supporting them.  You can use this information to download various artifacts of operating systems (e.g. ISO), generate Packer templates for supported platforms, or even automate your CI/CD infrastructure to maintain artifacts needed to build, test, and operate your applications.
 
Keep in mind, this is a work in progress, and we would love your contributions!  Please feel free to submit a pull request or file an issue if you have questions, ideas, or suggestions.  We're all in this together! 

## Specification

The specification looks like this

```yaml
name: Ubuntu
flavor: Server
downloads:
  - https://releases.ubuntu.com/22.04/ubuntu-22.04-live-server-amd64.iso
documentation: https://ubuntu.com/server/docs
architecture: amd64
release: 22.04
version: 22.04
hardware:
  memory: 512
  storage: 2560
  processors:
    count: 1
    cores: 1
hypervisors:
  vsphere:
    disk_controller_type: lsilogic
    firmware: bios
    guest_os_type: otherGuest64
    network_adapter_type: vmxnet3
```

The fields:

| Name         | Required | Notes                                                                                                                                  |
|--------------|----------|----------------------------------------------------------------------------------------------------------------------------------------|
| name         | yes      | The name of the operating system                                                                                                       |
| flavor       | no       | The flavor of the operating system                                                                                                     |
| downloads    | yes      | URLs where to download the operating system from                                                                                       |
| architecture | yes      | The architecture of the platform, for example `amd64`, `i386`, `mips`, `mips64`, `mips64le`                                            |
| release      | no       | The release of the operating system. When omitted it's assumed it's a rolling release, like *Arch Linux*.                              |
| version      | no       | The version of the operating system. When omitted it's assumed its a rolling version, such as *CentOS 8 Stream* and *CentOS 9 Stream*. |
| hardware     | no       | the minimum hardware requirements                                                                                                      |

The hardware is described as follows:

| Name       | Required | Default | Notes                                             |
|------------|----------|---------|---------------------------------------------------|
| memory     | no       | 2048    | It's specified in megabytes, so 2048 will be 2GB. |
| storage    | no       | 10240   | It's specified in megabytes, so 2048 will be 2GB. |
| processors | no       |         | See below                                         |

The processors are as follows:

| Name  | Required | Default | Notes                                       |
|-------|----------|---------|---------------------------------------------|
| count | no       | 1       | The number of processors                    |
| cores | no       | 1       | The number of processor cores per processor |

Hypervisors contain the following fields:

| Name    | Required | Default | Notes                       |
|---------|----------|---------|-----------------------------|
| vsphere | no       |         | Settings for VMware vSphere |


| Name                 | Required | Default      | Notes                              |
|----------------------|----------|--------------|------------------------------------|
| disk_controller_type | no       | lsilogic     | The type of disk controller to use |
| firmware             | no       | bios         | The type of firmware to use        |
| guest_os_type        | no       | otherGuest64 | The type of guest OS to use        |
| network_adapter_type | no       | vmxnet3      | The type of network adapter to use |

## Contributing

This is a work in progress, and we would love your contributions!  Please feel free to submit a pull request or file an issue if you have questions, ideas, or suggestions.  
