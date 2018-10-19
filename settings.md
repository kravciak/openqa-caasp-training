# Define settings in openQA

### Menu > Medium Types
```
Distri:  caasp
Version: 3.0
Flavor:  DVD
Arch:    x86_64

Settings:
BETA=0
DESKTOP=textmode
```

### Menu > Machines (change WORKER_CLASS)
```
Name:    caasp_x86_64
Backend: qemu

Settings:
HDDSIZEGB=40
QEMUCPU=host
QEMURAM=4096
WORKER_CLASS=caasp_x86_64_[1-3]
```

### Menu > Test suites
```yaml
# CaaSP-controller
+HDD_1=sle-12-SP3-Server-DVD-x86_64-gnome-CaaSP.qcow2
BOOT_HDD_IMAGE=1
CONTAINER_RUNTIME=docker
DESKTOP=gnome
NICTYPE=tap
NOAUTOLOGIN=1
STACK_ROLE=controller
SUPPORT_SERVER=1
SUPPORT_SERVER_ROLES=dhcp,dns,ntp
```

```yaml
# CaaSP-admin
EXTRABOOTPARAMS=hostname=admin
NICTYPE=tap
PARALLEL_WITH=CaaSP-controller
QEMUCPUS=2
STACK_ROLE=admin
SYSTEM_ROLE=admin
```

```yaml
# CaaSP-master-api
EXTRABOOTPARAMS=hostname=master-API
NICTYPE=tap
PARALLEL_WITH=CaaSP-controller
STACK_ROLE=worker
SYSTEM_ROLE=worker
```

```yaml
# CaaSP-worker-mixed
EXTRABOOTPARAMS=hostname=miXed
NICTYPE=tap
PARALLEL_WITH=CaaSP-controller
STACK_ROLE=worker
SYSTEM_ROLE=worker
```

```yaml
# CaaSP-worker-ay1
AUTOYAST=http://admin.openqa.test/autoyast
EXTRABOOTPARAMS=hostname=worker-ay1
NICTYPE=tap
PARALLEL_WITH=CaaSP-controller
STACK_ROLE=worker
SYSTEM_ROLE=worker
```

### Job Groups: Pair media & machine & test suites
Now you need to associate which test should be run on which image

# Run openQA jobs

### !!! Download GM image and support server
You need to have images that you want to test :)
```bash
cd /var/lib/openqa/share/factory/iso/
wget http://openqa.suse.de/tests/1785307/asset/iso/SUSE-CaaS-Platform-3.0-DVD-x86_64-Build0101-Media1.iso

cd /var/lib/openqa/share/factory/hdd/
wget http://openqa.suse.de/tests/1785307/asset/hdd/sle-12-SP3-Server-DVD-x86_64-gnome-CaaSP.qcow2
```

### Schedule all tests associated with image
Push local images to openQA scheduler. All settings have to be defined by you.
```bash
/usr/share/openqa/script/client isos post ISO=SUSE-CaaS-Platform-3.0-DVD-x86_64-Build0101-Media1.iso \
  DISTRI=caasp VERSION=3.0 FLAVOR=DVD ARCH=x86_64 BUILD=0101
```
