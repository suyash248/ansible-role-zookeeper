# [zookeeper](https://galaxy.ansible.com/suyash248/ansible_role_zookeeper) - Ansible role to install zookeeper.

#### Installation
```
ansible-galaxy install suyash248.ansible_role_zookeeper
```

#### Prerequisites
- **Java 1.8**

#### Settings/Variables

Following variables can be overwritten by passing `extra-vars` option, or by modifying `defaults/main.yml`, or in a template created using *ansible tower*.

```yaml
---
---
zookeeper_home: "/etc/installers/zookeeper"
zookeeper:
  home: "{{ zookeeper_home }}"
  version: 3.6.1
  scala_version: 2.13
  config_file: "zoo.cfg"
  data_dir: "{{ zookeeper_home }}/data/zookeeper"
  log_dir: "{{ zookeeper_home }}/logs"
  apt_cache_timeout: 3600
  client_port: 2181
  init_limit: 5
  sync_limit: 2
  tick_time: 2000
  hosts_file: "/etc/hosts"
  daemon:
    name: "zookeeper"
    type: "service" # systemctl
    start_on_boot: "yes" # no
```

#### Inventory/hosts
```
[zookeeper_hosts]
zookeeper1 ansible_host=91.28.240.78 alias=zookeeper1 private_ip=172.56.29.25 zookeeper_id=1 client_port=2181
zookeeper2 ansible_host=91.85.139.81 alias=zookeeper2 private_ip=172.45.12.83 zookeeper_id=2 client_port=2181
zookeeper3 ansible_host=91.46.152.93 alias=zookeeper3 private_ip=172.84.68.97 zookeeper_id=3 client_port=2181
```

#### Playbook
Sample playbook can be found in `zookeeper/tests` directory.

```yaml
---
- hosts: zookeeper_hosts
  vars:
  	ansible_python_interpreter: /usr/bin/python3
  roles:
  	- role: zookeeper
  	  become: yes
```

#### Test
```bash
$ bash bin/zkServer.sh status
/usr/bin/java
ZooKeeper JMX enabled by default
Using config: /etc/installers/zookeeper/bin/../conf/zoo.cfg
Client port found: 2181. Client address: localhost.
Mode: follower
```
