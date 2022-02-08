# Docker

## FAQ

**Q:** Remove unused data

```bash
docker system prune
```

**Q:** Prune images older than 8 months

```bash
docker image prune -a --filter "until=$((8 * 730))h"
```
