# Linux & Mac OS

## Server Information

```bash
uname -a # Linux server version and simple information 
uname -a # Linux kernel version
lsb_release -a # Unbutu release version 
lscpu # CPU information

ps huH p <PID_OF_U_PROCESS> | wc -l # Check Thread count of a process

scp [user]@[remote_server]:[remote_directory] [local]

du . -h --max-depth=1 | sort -hr | head -10 # find top 10 largest directories
ls -alh | sort -t '-' -k12 # Sort pb by timestmp
ls -alh | grep 'ch09020' | sort -t '-' -k12 # Sort pb by timestmp

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
