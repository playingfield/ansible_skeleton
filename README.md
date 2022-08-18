# ansible_skeleton
Skeleton for `ansible-galaxy role init`

```sh
pip install --user pre-commit tox
mkdir -p $HOME/git ~/.ansible/roles
cd $HOME/git
git clone https://github.com/playingfield/ansible_skeleton.git
cd ansible_skeleton
mv ansible.cfg $HOME/.ansible.cfg
cd ~/.ansible/roles
ansible-galaxy role init my_role
tox
cd my_role && git init && git add .
pre-commit install
pre-commit run --all-files
```
