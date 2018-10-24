# Define settings in openQA

**Replace <N> with your number (1 .. 7)**

### Menu > Medium Types  (change Distri)
This section defines ISO image. Flavor can distinguish net/live/normal types.
```yaml
Distri:  caasp<X>
Version: 3.0
Flavor:  DVD
Arch:    x86_64
Settings:
BETA=0
DESKTOP=textmode
```

### Menu > Machines
Definition of machine that should run our test. This matches real machine with openqa-worker installed that has set of capabilities (run on specific VM host, can run multimachine jobs, is x86_64)  
```yaml
Name:    caasp_x86_64
Backend: qemu
Settings:
HDDSIZEGB=40
QEMUCPU=host
QEMURAM=4096
WORKER_CLASS=caasp_x86_64
```

### Menu > Test suites
Test suite is set of variables given to the job when started. Variables are then parsed
```yaml
# MicroOS test (optional example)
Name: MicroOS-plain
Settings:
EXTRA=FEATURES
SYSTEM_ROLE=plain
```

```yaml
Name: CaaSP-controller
Settings:
+HDD_1=sle-12-SP3-Server-DVD-x86_64-gnome-CaaSP.qcow2
BOOT_HDD_IMAGE=1
CONTAINER_RUNTIME=docker
DESKTOP=gnome
NICTYPE=tap
NOAUTOLOGIN=1
STACK_ROLE=controller
SUPPORT_SERVER=1
SUPPORT_SERVER_ROLES=dhcp,dns,ntp

Name: CaaSP-admin
Settings:
EXTRABOOTPARAMS=hostname=admin
NICTYPE=tap
PARALLEL_WITH=CaaSP-controller
QEMUCPUS=2
STACK_ROLE=admin
SYSTEM_ROLE=admin

Name: CaaSP-master-api
Settings:
EXTRABOOTPARAMS=hostname=master-API
NICTYPE=tap
PARALLEL_WITH=CaaSP-controller
STACK_ROLE=worker
SYSTEM_ROLE=worker

Name: CaaSP-worker-mixed
Settings:
EXTRABOOTPARAMS=hostname=miXed
NICTYPE=tap
PARALLEL_WITH=CaaSP-controller
STACK_ROLE=worker
SYSTEM_ROLE=worker

Name: CaaSP-worker-ay1
Settings:
AUTOYAST=http://admin.openqa.test/autoyast
EXTRABOOTPARAMS=hostname=worker-ay1
NICTYPE=tap
PARALLEL_WITH=CaaSP-controller
STACK_ROLE=worker
SYSTEM_ROLE=worker
```

**Optional Add & Remove nodes**

```yaml
Name: CaaSP-worker-addrm
Settings:
DELAYED=worker
EXTRABOOTPARAMS=hostname=worker-addrm
NICTYPE=tap
PARALLEL_WITH=CaaSP-controller
STACK_ROLE=worker
SYSTEM_ROLE=worker
```

```yaml
Name: CaaSP-master-rm
Settings:
EXTRABOOTPARAMS=hostname=master-RM
NICTYPE=tap
PARALLEL_WITH=CaaSP-controller
STACK_ROLE=worker
SYSTEM_ROLE=worker

Name: CaaSP-master-add
Settings:
DELAYED=master
EXTRABOOTPARAMS=hostname=master-add
NICTYPE=tap
PARALLEL_WITH=CaaSP-controller
STACK_ROLE=worker
SYSTEM_ROLE=worker

Name: CaaSP-master-ay
Settings:
AUTOYAST=http://admin.openqa.test/autoyast
EXTRABOOTPARAMS=hostname=master-ay
NICTYPE=tap
PARALLEL_WITH=CaaSP-controller
STACK_ROLE=worker
SYSTEM_ROLE=worker
```


### Job Groups: Pair media & machine & test suites
Now you need to associate which test should be run on which image

# Run openQA jobs

### Download GM image and support server
First download image that you want to test. You can download from:
 - https://openqa.suse.de/group_overview/136
 - http://download.suse.de/install/SUSE-CaaSP-3-GM/
```bash
# We downloaded GM image & support-server
# cd /var/lib/openqa/share/factory/iso/
# wget http://openqa.suse.de/tests/1785307/asset/iso/SUSE-CaaS-Platform-3.0-DVD-x86_64-Build0101-Media1.iso

# cd /var/lib/openqa/share/factory/hdd/
# wget http://openqa.suse.de/tests/1785307/asset/hdd/sle-12-SP3-Server-DVD-x86_64-gnome-CaaSP.qcow2
```

### Schedule all tests associated with image
Push local images to openQA scheduler. All settings have to be defined by you.
```bash
# Change DISTRI and optionally BUILD variable
/usr/share/openqa/script/client isos post ISO=SUSE-CaaS-Platform-3.0-DVD-x86_64-Build0101-Media1.iso \
  DISTRI=caasp<N> VERSION=3.0 FLAVOR=DVD ARCH=x86_64 BUILD=0101

# Official openqa.suse.de
sudo -u geekotest -i ./rsync.pl --host localhost --verbose --add-existing caasp_dvd
```

# Files
```
├── lib
    ├── caasp.pm
    ├── caasp_controller.pm
├── data
    ├── caasp/*
├── tests
    ├── caasp/*
    ├── caasp/stack*
```

# Tips
```bash
# connect to running job
PORT=5990+worker_id
vncviewer uv300x.arch.suse.de:6019 -shared

# keep cluster alive in case of failure
DEBUG_SLEEP=controller
```

# What we have
 - CaaSP   - https://openqa.suse.de/tests/overview?distri=caasp&version=3.0&build=0098&groupid=134 
 - MicroOS - https://openqa.suse.de/tests/overview?distri=caasp&version=3.0&build=0101&groupid=136

# Tasks
 - fix installation workflow for CaaSP 4.0 (OCI -> SLES installer)
 - add Helm test
 - add CAP deployment
 - add drbd storage to support-server (use it later as storage class)
 - backup & restore of admin node
