# Connect to openQA
ssh credentials: root:susetesting

```bash
# openqa-webui:
http://uv300x.arch.suse.de:81/

# Location of tests
ssh root@uv300x.arch.suse.de -p 2201 -4
```

# Schedule single machine job with clone_job.pl
 - Good for single jobs
 - magic for multimachine jobs
 - impossible for clusters
 
It downloads image and schedules it. Copies all settings from remote job.
```bash
# https://openqa.suse.de/tests/1783034 (MicroOS)
sudo /usr/share/openqa/script/clone_job.pl --from https://openqa.suse.de --host localhost 1783034
```

# Tasks
 - fix CaaSP 4.0 = update installation workflow
 - add Helm test
 - add CAP deployment
 - add drbd storage to support-server (use it later as storage class)
 - backup & restore of admin node
