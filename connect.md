# Connect to openQA
ssh credentials: root:susetesting

```bash
openqa-webui-1:
  192.168.100.191
  http://uv300x.arch.suse.de:81/
  ssh root@uv300x.arch.suse.de -p 2201

openqa-webui-2:
  192.168.100.222
  http://uv300x.arch.suse.de:82/
  ssh root@uv300x.arch.suse.de -p 2202

openqa-webui-3:
  192.168.100.228
  http://uv300x.arch.suse.de:83/
  ssh root@uv300x.arch.suse.de -p 2203

openqa-webui-4:
  192.168.100.???
  http://uv300x.arch.suse.de:84/
  ssh root@uv300x.arch.suse.de -p 2204
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
