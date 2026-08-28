# OrbitE — TII OrbitSight Challenge

Event-native, CPU-only resident space object (RSO) detection and tracking from raw neuromorphic
vision sensor (NVS) event streams. One offline Docker image — no GPU, no network.

## Docker image

The image is published as a release asset (it exceeds GitHub's 100 MB file limit for normal files):

**[Download the v14 release »](../../releases/tag/v14)**

- `orbite-orbitsight-v14.tar.gz` — the image, exported with `docker save` and gzipped (~146 MB)
- `orbite-orbitsight-v14.tar.gz.sha256` — checksum

```bash
# verify, load, and run offline
sha256sum -c orbite-orbitsight-v14.tar.gz.sha256
docker load -i orbite-orbitsight-v14.tar.gz

docker run --rm \
  -v /path/to/OrbitSight_dataset:/OrbitSight_dataset:ro \
  -v /path/to/work:/work \
  orbite-orbitsight:v14
```

The container reads the NVS recordings from `/OrbitSight_dataset` (read-only) and writes the
organizer prediction files, the scoring workbook, track files, runtime metrics and a self-contained
HTML report to `/work/<team>/<DDMMYYYY>`. It runs fully offline.

sha256: `28e24c3635a9fac715cdc251fb2209a540b93b4bd361e1a9d421287174252889`
