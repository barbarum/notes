# Git

## Tagging & Release

```bash
git tag -a v0.0.2 -m "Releasing version v0.0.2"
git push origin v0.0.2
```

## Gitlab Runner

```bash
docker run -d --name gitlab-runner --restart always -v /srv/gitlab-runner/config:/etc/gitlab-runner -v /var/run/docker.sock:/var/run/docker.sock gitlab/gitlab-runner:latest -p 8093:8093 #Start gitlab runner for registry
```

## FAQ

1. Remove tracking branches no longer exists on remote

```bash
git fetch -p && \
    for branch in $(git for-each-ref --format '%(refname) %(upstream:track)' refs/heads | awk '$2 == "[gone]" {sub("refs/heads/", "", $1); print $1}'); \
    do git branch -D $branch; \
    done
```

2. Sign off git commit `git commit -s`
3. Sign off git merge `git merge --signoff`
