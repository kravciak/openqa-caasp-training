# Run openQA jobs

We already tried clone_job.pl

## Download GM image and support server
You need to have images that you want to test :)
```bash
cd /var/lib/openqa/share/factory/iso/
wget https://openqa.suse.de/tests/1785307/asset/iso/SUSE-CaaS-Platform-3.0-DVD-x86_64-Build0101-Media1.iso

cd /var/lib/openqa/share/factory/hdd/
wget https://openqa.suse.de/tests/1785307/asset/hdd/sle-12-SP3-Server-DVD-x86_64-gnome-CaaSP.qcow2
```

## Schedule all tests associated with image
Push local images to openQA scheduler. All settings have to be defined by you.
```bash
/usr/share/openqa/script/client isos post ISO=SUSE-CaaS-Platform-3.0-DVD-x86_64-Build0101-Media1.iso \
  DISTRI=caasp VERSION=3.0 FLAVOR=DVD ARCH=x86_64 BUILD=0101
```

## Rsync script (that's how openQA does it)
Download images from defined repository, add some test settings and calls "client isos post ..."
```bash
sudo -u geekotest -i ./rsync.pl --host localhost --verbose --add-existing caasp_dvd
```
