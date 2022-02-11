# Common Used Commands

## Run command behind proxy

```bash
export http_proxy=http://{host:port};export https_proxy=http://{host:port};export ALL_PROXY=socks5://{host:port} # Set proxies for terminal commands
# Config git to run behind proxy only.
git config --global http.proxy http://{host:port}
# Run a pip command behind proxy only. 
pip install --proxy=http://{host:port} {some-package}
```

## Tmux

```bash
tmux new -s <session id> # Open a new tmux session 'default'
# Detach current tmux session: Ctrl + b -> d
tmux ls # List all tmux sessions 
tmux a -t <session id>
```
