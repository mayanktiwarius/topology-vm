Sample readme
# topology-vm

Steps to create a VM with the topology package installed.
1. Sync the topology package to the VM
git submodule update --init --recursive
2. Bring up vagrant
vagrant up
3. Connect to vagrant vm
vagrant ssh
4. Bring up the pods
cd topology/leafspine
make build
make up
5. Reflect the change done on the host to the container
vagrant rsync
6. Bring down the cluster
make down


