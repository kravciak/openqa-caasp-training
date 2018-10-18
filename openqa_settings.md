Medium Types:
Distri: caasp
Version: 3.0
Flavor: DVD
Arch: x86_64
Settings:
    BETA=0
    DESKTOP=textmode
    MAX_JOB_TIME=10800
    REGCODE=43678356f84d44e6

Machines:
Name: caasp_x86_64
Backend: qemu
Settings:
    HDDSIZEGB=40
    QEMUCPU=host
    QEMURAM=4096
    WORKER_CLASS=caasp_x86_64

Test suites:
CaaSP-controller
    +HDD_1=sle-12-SP3-Server-DVD-x86_64-gnome-CaaSP.qcow2
    BOOT_HDD_IMAGE=1
    CONTAINER_RUNTIME=docker
    DESKTOP=gnome
    NICTYPE=tap
    NOAUTOLOGIN=1
    STACK_ROLE=controller
    SUPPORT_SERVER=1
    SUPPORT_SERVER_ROLES=dhcp,dns,ntp
    WORKER_CLASS=tap

CaaSP-admin
    EXTRABOOTPARAMS=hostname=admin
    NICTYPE=tap
    PARALLEL_WITH=CaaSP-controller
    QEMUCPUS=2
    STACK_ROLE=admin
    SYSTEM_ROLE=admin
    WORKER_CLASS=tap

CaaSP-master-api
    EXTRABOOTPARAMS=hostname=master-API
    NICTYPE=tap
    PARALLEL_WITH=CaaSP-controller
    STACK_ROLE=worker
    SYSTEM_ROLE=worker
    WORKER_CLASS=tap

CaaSP-worker-mixed
    EXTRABOOTPARAMS=hostname=miXed
    NICTYPE=tap
    PARALLEL_WITH=CaaSP-controller
    STACK_ROLE=worker
    SYSTEM_ROLE=worker
    WORKER_CLASS=tap

CaaSP-worker-ay1
    AUTOYAST=http://admin.openqa.test/autoyast
    EXTRABOOTPARAMS=hostname=worker-ay1
    NICTYPE=tap
    PARALLEL_WITH=CaaSP-controller
    STACK_ROLE=worker
    SYSTEM_ROLE=worker
    WORKER_CLASS=tap

Job Groups: Pair media & machine & test suites