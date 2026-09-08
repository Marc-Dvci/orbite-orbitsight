# OrbitE, TII OrbitSight Challenge

Event-native, CPU-only resident space object (RSO) detection and tracking from raw neuromorphic
vision sensor (NVS) event streams. One offline Docker image, no GPU and no network.

## Docker image

The image is published as a release asset (it exceeds GitHub's 100 MB file limit for normal files):

**[Download the v15 release »](../../releases/tag/v15)**

- `orbite-orbitsight-v15.tar.gz`, the image exported with `docker save` and gzipped (~146 MB)
- `orbite-orbitsight-v15.tar.gz.sha256`, the checksum

```bash
# verify, load, and run offline
sha256sum -c orbite-orbitsight-v15.tar.gz.sha256
docker load -i orbite-orbitsight-v15.tar.gz

docker run --rm \
  -v /path/to/OrbitSight_dataset:/OrbitSight_dataset:ro \
  -v /path/to/work:/work \
  orbite-orbitsight:v15
```

The container reads the NVS recordings from `/OrbitSight_dataset` (read-only) and writes the
organizer prediction files, the scoring workbook, track files, runtime metrics and a self-contained
HTML report to `/work/<team>/<DDMMYYYY>`. It runs fully offline.

The image carries its own documentation at `/app`: `README.md`, `docs/VALIDATION.md`,
`docs/IMPLEMENTATION_AUDIT.md`, `docs/PROVENANCE.md` and `docs/THEOREMS_17_18_EVENT_LAYER.md`. Every
run also copies them into `documentation/` inside the results folder.

Detection accuracy on the four unseen test recordings, scored by the organizer's `evaluate.py`:
mAP@0.5 0.5709, precision 0.5918, recall 0.7250, F1 0.6516. Worst p95 22.9 ms per 40 ms window.

sha256: `ee6b7ff5ef768a74a95dc297307fc098c8332d59dc33c9005f49c0127914d053`
