# Overview

Installs ZooKeeper servers with Exhibitor service monitoring & S3 backed shared configuration.

# Requirements

* Ubuntu 16.04 or later for ZooKeeper nodes
* Systemd for Exhibitor service management
* Ansible 2.0 or later
* Ansible inventory, with ZooKeeper nodes in a "zookeeper" group and:
    Node variables for ZooKeeper nodes:
    * zookeeper_id (Zookeeper ID)
    Shared variables for ZooKeeper nodes:
    * s3_config_location (S3 shared config (BUCKET:KEY))
    * s3_access_key (S3 access key)
    * s3_secret_key (S3 secret key)
    * heading_text (heading text for Exhibitor UI)
    * zoo_cfg_extra (extra ZooKeeper cfg, defaults to 'syncLimit=5&tickTime=2000&initLimit=10') [OPTIONAL]
    * java_opts (Java options) [OPTIONAL]
    * proxy_env (proxy configuration, used for package installations) [OPTIONAL]
    * exhibitor_s3_endpoint (S3 endpoint if using non-AWS S3) [OPTIONAL]

# Installation

Create a S3 bucket for shared configuration storage.

Run Ansible to provision ZooKeeper:

ansible-playbook -i inventory_file zookeeper.yml

## Using non-AWS S3

You can use non-AWS S3 (e.g. RiakCS), by setting the 'exhibitor_s3_endpoint' to point to your S3 environment.

## Running in private cloud / behind NAT

If the public address/IP of you node is different that the local address/IP, you'll probably need to set
the following extra config using zoo_cfg_extra: "quorumListenOnAllIPs=true&clientPortBindAddress=0.0.0.0"
This will allow ZooKeeper to startup when the public address/IP isn't bindable on the node.

# TODO

* Build Exhibitor jar on deployment node (don't pre-package)

# License

Copyright (c) 2017 Lekane Oy. All rights reserved.

Redistribution and use in source and binary forms, with or without
modification, are permitted provided that the following conditions are
met:

   * Redistributions of source code must retain the above copyright
notice, this list of conditions and the following disclaimer.
   * Redistributions in binary form must reproduce the above
copyright notice, this list of conditions and the following disclaimer
in the documentation and/or other materials provided with the
distribution.
   * Neither the name of Lekane Oy nor the names of its
contributors may be used to endorse or promote products derived from
this software without specific prior written permission.

THIS SOFTWARE IS PROVIDED BY THE COPYRIGHT HOLDERS AND CONTRIBUTORS
"AS IS" AND ANY EXPRESS OR IMPLIED WARRANTIES, INCLUDING, BUT NOT
LIMITED TO, THE IMPLIED WARRANTIES OF MERCHANTABILITY AND FITNESS FOR
A PARTICULAR PURPOSE ARE DISCLAIMED. IN NO EVENT SHALL THE COPYRIGHT
OWNER OR CONTRIBUTORS BE LIABLE FOR ANY DIRECT, INDIRECT, INCIDENTAL,
SPECIAL, EXEMPLARY, OR CONSEQUENTIAL DAMAGES (INCLUDING, BUT NOT
LIMITED TO, PROCUREMENT OF SUBSTITUTE GOODS OR SERVICES; LOSS OF USE,
DATA, OR PROFITS; OR BUSINESS INTERRUPTION) HOWEVER CAUSED AND ON ANY
THEORY OF LIABILITY, WHETHER IN CONTRACT, STRICT LIABILITY, OR TORT
(INCLUDING NEGLIGENCE OR OTHERWISE) ARISING IN ANY WAY OUT OF THE USE
OF THIS SOFTWARE, EVEN IF ADVISED OF THE POSSIBILITY OF SUCH DAMAGE.

