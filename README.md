`dimmaryanto93.sonatype_nexus_oss_registry`
=========

Repository ini digunakan untuk meng-konfigurasi registry pada Sonatype Nexus OSS menggunakan Rest API seperti 

- docker
- maven
- npm
- dan lain-lain

Ansible - User Guide
------------

Persiapan yang harus di lalukan, diantaranya

1. Create new user on your server, Recomend using **very-very Strong Password** or using password generator. 
  ```bash
  adduser <username>
  ```

2. Granted to sudoers with NOPASSWD, using `visudo`
  ```ini
  username    ALL=(ALL) NOPASSWD:ALL
  ```

3. Authenticate with private-key for login ssh, generate ssh key on your local machine then use `ssh-copy-id user@your-ip-server` to copy public key to your server.


Requirements
------------

Untuk menggunakan role ini, kita membutuhkan package/collection 

- [ansible.posix](https://github.com/ansible-collections/ansible.posix)
- [community.general](https://github.com/ansible-collections/community.general)

Temen-temen bisa install, dengan cara 

```bash
ansible-galaxy collection install ansible.posix community.general
```

Atau temen-temen bisa menggunakan `requirement.yaml` file and install menggunakan `ansible-galaxy collection install -r requirement.yaml`, dengan format seperti berikut:

```yaml
---
collections:
  - community.general
  - ansible.posix
```

Role Variables
--------------

Ada beberapa variable yang temen-temen bisa gunakan untuk setting sonatype nexus-oss, diantaranya seperti berikut:

| Variable name                 | Example value       | Description |
| :---                          | :---                | :---        |


Dependencies
------------

None


Example Playbook
----------------

Including an example of how to use your role (for instance, with variables passed in as parameters) is always nice for users too:

```ansible
- hosts: servers
  vars:
    nexus_admin_user: admin
    nexus_admin_password: admin123
    nexus_default_host: 'localhost'
    nexus_default_port: '8081'
    nexus_registry_docker_enabled: true
    docker_registry_hosted_name: 'docker-registry'
    docker_registry_hosted_port: '8087'
    docker_registry_group_name: 'docker-public-group'
    docker_registry_group_port: '8086'
    nexus_registry_docker_repositories: []
  roles:
    - dimmaryanto93.sonatype_nexus_oss_registry 
```

License
-------

MIT
