# Makefile for ansible execution environments using ansible-runner
# export RUNTIME=docker to override
RUNTIME ?= podman
BASE_NAME=ansible-runner
ANSIBLE_RUNNER_IMAGE=quay.io/ansible/ansible-runner:stable-2.12-latest

.PHONY standalone:
standalone:
	ansible-runner run playbooks -p playbook.yml

.PHONY python_interface:
python_interface:
	./play.py

.PHONY build:
build:
	ansible-builder build --build-arg ANSIBLE_RUNNER_IMAGE=${ANSIBLE_RUNNER_IMAGE} -t ${BASE_NAME} -c context --container-runtime ${RUNTIME}

.PHONY bash:
bash:
	${RUNTIME} run --rm --network=host -ti -v${HOME}/.ssh:/root/.ssh -v ${PWD}/playbooks:/runner ${BASE_NAME} bash

.PHONY run:
run:
	${RUNTIME} run --rm --network=host -ti -v${HOME}/.ssh:/root/.ssh -v ${PWD}/playbooks:/runner -e RUNNER_PLAYBOOK=playbook.yml ${BASE_NAME}

clean:
	rm -rf .venv context playbooks/artifacts/*
