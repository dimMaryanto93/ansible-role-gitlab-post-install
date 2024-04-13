`dimmaryanto93.gitlab_post_install`
=========

Repository ini digunakan untuk meng-konfigurasi gitlab seperti

- Gitlab instance variables for `M2_SETTINGS_XML`, `DOCKER_CONF_JSON`, `SONAR_URL` and more
- Configure gitlab settings

Ansible - User Guide
------------

Persiapan yang harus di lalukan, diantaranya

1. Authenticate with private-key for login ssh, generate ssh key on your local machine then use `ssh-copy-id user@your-ip-server` to copy public key to your server.
2. Create personal access token for user `root` on Gitlab repository
  - Grant privileges is `api`, `read_api`, `read_user`, `create_runner`, `k8s_proxy`, `read_repository`, `write_repository`, `sudo`, `admin_mode` and give it name `tokenForAdmin` look like this:
    ![gitlab-permission](docs/01a-grant-privileges.png)
  - Set personal access token to variables: `gitlab_private_access_token`
3. Create access token for user `admin` on Sonarqube
  - Set the token to variables: `sonarqube_auth_token`
4. Setup auth for docker registry
  - Set username & password to variable: `docker_registry_login_secret`

Requirements
------------

Untuk menggunakan role ini, kita membutuhkan package/collection 

- None

Role Variables
--------------

Ada beberapa variable yang temen-temen bisa gunakan untuk setting sonatype nexus-oss, diantaranya seperti berikut:

| Variable name                   | Example value       | Description |
| :---                            | :---                | :---        |
| `docker_registry_domain`        | `private.nexus-registry.docker.local` | Default domain for docker registry |
| `docker_registry_login_secret`  | `admin:password`    | change this to your docker registry auth the format is <username>:<password> |
| `gitlab_private_access_token`   | `ChangedMe` | **No default value for this**, please generate the access token from gitlab on personal access token, see tutorial below |
| `sonarqube_auth_token`          | `ChangedMe`         | **No default value for this**, please generate the access token from sonarqube on System -> access token, see tutorial below |
| enabled_gitlab_config_variables_instance  | `true` or `false` | SET to true if you want setup config CI/CD Variables on instance level |
| `nexus_default_schema`          | `http`              | Default protocol for nexus oss |
| `nexus_default_host`            | `localhost`         | Default host address for nexus oss |
| `nexus_default_port`            | `8081`              | Default port for nexus oss repository |
| `nexus_admin_user`              | `admin`             | Default user for auth nexus oss repository |
| `nexus_admin_password`          | `admin123`          | Default password for auth nexus oss repository |
| `sonarqube_proto`               | `http`              | Default protocol for sonarqube |
| `sonarqube_host`                | `localhost`         | Default host for sonarqube |
| `sonarqube_port`                | `9000`              | Default port for sonarqube  |
| `sonarqube_auth_token`          | `ChangedMe`         | **No default value for this**, please generate access token for sonarqube |

Dependencies
------------

- None


Example Playbook
----------------

Including an example of how to use your role (for instance, with variables passed in as parameters) is always nice for users too:

```ansible
- hosts: ['all']
  vars:
    gitlab_address: localhost
    docker_registry_login_secret: "user:passwordnyaUs3r"
    gitlab_private_access_token: "glpat-R4KpspJXvyAq6QZHsREG"
    sonarqube_auth_token: default
  roles:
    - dimmaryanto93.gitlab_post_install
```

License
-------

MIT
