# OCP4 UPI Helper Node Playbook

This assumes the following

1. You're on a Network that has access to the internet
2. The network you're on does NOT have DHCP
3. The helpernode will be your LB/DHCP/DNS and HTTPD server
4. You still have to do the OpenShift Install steps by hand (this just sets up the node to help you)
5. I used CentOS 7
6. You will be running the `openshift-install` command from this helpernode


To use this...install a CentOS 7 server with 4 vCPUs, 4 GB of RAM, and 50GB HD...then....

```
yum -y install ansible git
git clone https://github.com/christianh814/ocp4-upi-helpernode
cd ocp4-upi-helpernode
```

Inside that dir there is a `vars.yaml` ... **__modify it__** to match your network (the example one assumes a `/24`)


Run the playbook

```
ansible-playbook -e @vars.yaml tasks/main.yml
```

Once it's ran, check if the DNS is okay with the checker script

```
./dns-checker.sh  <domain> <clusterid>
```

Now you're ready to follow the [OCP4 UPI install doc](https://docs.openshift.com/container-platform/4.1/installing/installing_bare_metal/installing-bare-metal.html#ssh-agent-using_installing-bare-metal)
