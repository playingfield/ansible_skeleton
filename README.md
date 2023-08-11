# Ansible role skeleton
Skeleton for `ansible-galaxy role init`

# Using the template
This template is designed for desired_state convergence with molecule.

`desired_state` is a variable that drives the role.
`present` is the default, and absent is the alterative for `desired_state`.

The template is very generic for a systemd service installed from a corresponding package.
Note that the tasks are split by state, for convergence, and that verify always runs.

These 2 files control most of the play:
- `tasks/main.yml`
- `handlers/main.yml`


To try it:

```sh
ansible-galaxy role init httpd
cd httpd
molecule converge
molecule converge -- -e desired_state=absent
```

The same thing works for Nginx:
```sh
ansible-galaxy role init nginx
molecule test
```

# Configure first!

In a codespace

```bash
cp ansible.cfg ~
```

## On your own machine

```sh
mkdir -p $HOME/git ~/.ansible/roles
cd $HOME/git
git clone https://github.com/playingfield/ansible_skeleton.git
```
Add these lines to your ~/.ansible.cfg
```ini
[galaxy]
role_skeleton = ~/git/ansible_skeleton/role
role_skeleton_ignore = ^.git$,^.*/.git_keep$,README.md
```

## matrix testing in a generated role

```sh
pip3 install --user tox
# edit tox.ini for a relevant setup
tox
```

## pre-commit hooks in a generated role

```sh
pip3 install --user pre-commit
# edit .pre-commit-config.yaml for a relevant setup
git init
pre-commit install
git add .
commit -m "initial commit"
pre-commit run --all-files
```
