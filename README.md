# DevOp in a Box

## Overview

Testing out the TIER IAM stack or DevOps (Jenkins or Docker) has never been easier.

TODO

## Starting Up

1. Create some VMs:

    ```bash
    $ vagrant up
    Bringing machine 'admin-swarm' up with 'parallels' provider...
    Bringing machine 'jenkins-worker-1' up with 'parallels' provider...
    Bringing machine 'iam-swarm-mngr-1' up with 'parallels' provider...
    Bringing machine 'iam-swarm-wrkr-1' up with 'parallels' provider...
    ==> admin-swarm: Registering VM image from the base box 'generic/centos7'...
    ...
    ```

1. Deploy the DevOps environment:

    ```bash
    $ docker run -it --rm -v ~/.vagrant.d/insecure_private_key:/private_key -v $(pwd):/ansible -w /ansible ansible/ansible-runner ansible-playbook project/test.yml -i inventory/hosts
    PLAY [all] ***************************************************************************
    TASK [Gathering Facts] ***************************************************************
    ok: [iam-swarm-mngr-1]
    ok: [jenkins-worker-1]
    ok: [admin-swarm]
    ok: [iam-swarm-wrkr-1]
    ...
    PLAY RECAP ***************************************************************************
    admin-swarm                : ok=47   changed=31   unreachable=0    failed=0
    iam-swarm-mngr-1           : ok=51   changed=33   unreachable=0    failed=0
    iam-swarm-wrkr-1           : ok=16   changed=11   unreachable=0    failed=0
    jenkins-worker-1           : ok=24   changed=13   unreachable=0    failed=0
    ```

1. Enjoy your DevOps environment. (See Applications/Endpoints section below, I recommend starting with the visualizer apps)

## Applications/Endpoints

### Visualizer (Admin Swarm)

- URL: http://10.211.56.10:8080/

### Jenkins (Admin Swarm)

- URL: <https://10.211.56.10:8443>
- Username: `admin`
- Password: `password`

### Docker Registry (Admin Swarm)

- URL: <https://10.211.56.10>
- Username: `admin`
- Password: `password`

### Shibboleth IdP (IAM Swarm)

- URL: https://10.211.56.20:4443/idp/
- Accounts:
  - Username/Password: `banderson` / `password`
  - Username/Password: `jgasper` / `password`
  - Username/Password: `jamith` / `password`

### Visualizer (IAM Swarm)

- URL: http://10.211.56.20:8080/

## Miscellanious Actions

### SSH Access to the VMs

> See `inventory/hosts` for each hosts' IP Address.

```bash
ssh -i ~/.vagrant.d/insecure_private_key vagrant@10.
```

### Tear Down the Environment

> `-f` will destroy the VMs without prompting the user for approval.

```bash
vagrant destroy -f
```
