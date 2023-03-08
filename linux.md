# Linux & Mac OS

## Server Information

```bash
uname -a # Linux server version and simple information 
uname -a # Linux kernel version
lsb_release -a # Unbutu release version 
lscpu # CPU information

ps huH p <PID_OF_U_PROCESS> | wc -l # Check Thread count of a process

scp [user]@[remote_server]:[remote_directory] [local]

xargs -0 printf '%s\n' </proc/1/cmdline # Print full command line of a specific process
```

### Date, Time, TZ

```bash
# Retrieve all available time zone 
cd /usr/share/zoneinfo/posix && find * -type f -or -type l | sort
```

### Networking 

```bash
netstat -tulpn | grep LISTEN # check all open ports

# dns resolve
nslookup bing.com
ping -c 4 bing.com
host bing.com
dig bing.com
curl -Ivs https://www.bing.com/
```

### Disk

```bash
du . -h --max-depth=1 | sort -hr | head -10 # find top 10 largest directories
du -sh /var # count the directory size
ls -alh | sort -t '-' -k12 # Sort pb by timestmp
ls -alh | grep 'ch09020' | sort -t '-' -k12 # Sort pb by timestmp

# For simple sequential I/O performance
## Measure the server throughtput (write speed)
echo /opt/airflow/logs/test1.img | awk '{printf "dd if=/dev/zero of=%s bs=1G count=1 oflag=dsync && rm -rf %s\n",$1, $1}' | xargs -0 bash -c
## Measure server latency
echo /opt/airflow/logs/test1.img | awk '{printf "dd if=/dev/zero of=%s bs=64K count=1000 oflag=dsync && rm -rf %s\n",$1, $1}' | xargs -0 bash -c

# For read performance
flush
echo 3 | sudo tee /proc/sys/vm/drop_caches
time dd if=/path/to/bigfile of=/dev/null bs=64k

rsync --delete-before -a [empty_directory] [dir_to_delete] # Delete large directory
ls -1 | xargs -I{} echo "rm -rf [Always use absolute path]/{}"
```

### Docker

```bash
docker system prune # clean up dangling docker images
```

### Nvidia GPU

```bash
nvidia-smi
```

## Singleview pb data output

```bash

git pull -r 
ssync.sh -f . -t dwei@gpu604.aibee.cn:~/aibee/singleview 

```
