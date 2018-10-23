# Connect to openQA

```bash
# openqa-webui:
http://uv300x.arch.suse.de:81/

# Location of tests (credentials: root:susetesting)
ssh root@uv300x.arch.suse.de -p 2201 -4
```

# Schedule single machine job with clone_job.pl
 - Good for single jobs
 - magic for multimachine jobs
 - impossible for clusters
 
It downloads image and schedules it. Copies all settings from remote job.
```bash
# https://openqa.suse.de/tests/1783034 (MicroOS 3.0)
/usr/share/openqa/script/clone_job.pl --from openqa.suse.de --host localhost 1783034

# https://openqa.suse.de/tests/2200622 (MicroOS 4.0)
/usr/share/openqa/script/clone_job.pl --from openqa.suse.de --host localhost 2200622
```
