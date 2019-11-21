# MBWU-Ceph

A playbook to Evaluate Ceph Performance with MBWU-based methodology.

This playbook uses [ceph-deploy](https://github.com/ceph/ceph-deploy) to install Ceph Nautilus.


## Prerequisites

1. The control node (on which the playbook will be run) has the following packages installed:
   - `ansible >= 2.7.9`
   - `python3-apt` or `python-apt`
   - `python3-netaddr` or `python-netaddr`

   `python-XXX` or `python3-XXX` depends on the python version of your ansible installer (`ansible --version`).

2. The control node can password-less ssh to all ceph nodes with users have password-less sudo privilege (including root, although this is NOT recommended). You can follow these sections to create a ceph deploy user:
   1. [`CREATE A CEPH DEPLOY USER`](https://docs.ceph.com/docs/master/start/quick-start-preflight/#create-a-ceph-deploy-user)
   2. [`ENABLE PASSWORD-LESS SSH`](https://docs.ceph.com/docs/master/start/quick-start-preflight/#enable-password-less-ssh)


## How to Run

```bash
git clone https://github.com/ljishen/MBWU-Ceph.git
cd MBWU-Ceph 
```

Then edit `hosts.yml` to add hosts for `osds`, `mons`, `mgrs`, and `admins`. Make sure that the `ansible_user` is specified for each host and meets Prerequisites 2). 

Now you can run:

```bash
ansible-playbook playbooks/site.yml [-v] [--tags teardown]
```
   - Providing `-v` to the command if you want to observe verbose outputs.
   - `--tags teardown` is used for clearing out Ceph installation and configurations.


## Troubleshooting

- **msg: 'Could not import python modules: apt, apt_pkg. Please install python3-apt package.'**

  ```
  1. Check if you have installed the python3-apt package.
  2. If you are uring `virtualenv`, make sure to create the virtual environment with `--system-site-packages`.
  ```

  For more information, check out this [ansible issue #14468](https://github.com/ansible/ansible/issues/14468).
