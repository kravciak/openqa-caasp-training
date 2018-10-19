# CaaSP in OpenQA

Deployment test needs at least 4 machines that communicate using tap devices.
- 1 controller node
- 1 admin node
- 1-3 master nodes
- 2-n minion nodes

Jobs must be run in certain order, that is provided by mutexes and barriers. Their initialization is in main.pm file.

![openqa](/openqa.png)


### Controller
It's heavily customized SLES-12-SP2 image acting as support server that provides DHCP, DNS, NTP support. Also contains customized firefox to display admin dashboard and bootstrap cluster.
After succesful bootstrap it runs basic kubernetes tests and deploys nginx application.

### Admin dashboard
CaaSP image installed as administration node. It contains velum dashboard and needs to be installed and set up before autoyast installation of cluster nodes.

### Cluster nodes
After administration node is installed and velum starts we can install cluster nodes. After installation finishes cluster can be bootstrapped.

- autoyast nodes do not have hostname from DHCP and they use default 'linux' hostname (bsc#1031623)
- node installed with hostname=master is later selected as master node
- node installed with hostname=node1 is late used for accessing the cluster in firefox

## HW Requirements
On medium (default for all nodes):
 - QEMURAM=4096
 - HDDSIZEGB=40

On admin test (applied only for admin):
 - QEMURAM=8192
 - QEMUCPUS=4

If you use more CPUs/RAM/DISK please make sure that you have underlying HW that can handle it!
