# Connect to openQA
 - ssh root@uv300x.arch.suse.de:$PORT
 - http://uv300x.arch.suse.de:$PORT

# Schedule single machine job with clone_job.pl
 - Good for single jobs
 - magic for multimachine jobs
 - impossible for clusters
 
It downloads image and schedules it. Copies all settings from remote job.
```bash
# https://openqa.suse.de/tests/1783034 (MicroOS)
sudo /usr/share/openqa/script/clone_job.pl --from https://openqa.suse.de --host localhost 1783034
```