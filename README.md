# ESPlab WebUI

[![release](https://img.shields.io/github/v/release/ESPlab-labs/ESPlab-WebUI)](https://github.com/ESPlab-labs/ESPlab-WebUI/releases)
[![license](https://img.shields.io/github/license/ESPlab-labs/ESPlab-WebUI)](LICENSE)

The web dashboard for [ESPlab](https://github.com/ESPlab-labs/ESPlab)
clusters. Point a browser at the machine the boards are plugged into and
see the whole cluster — boards, jobs, storage and the machine log — and
drive it: submit jobs, store data, watch work move between boards.

[ESP On Demand](https://github.com/ESPlab-labs/ESP-On-Demand), the media
server for ESPlab, runs on top of this dashboard.

[Releases](https://github.com/ESPlab-labs/ESPlab-WebUI/releases) ·
[Issues](https://github.com/ESPlab-labs/ESPlab-WebUI/issues)

## Features

- **Live cluster view** — boards with chip type and capacity, running jobs,
  pooled storage, machine log.
- **Drive the machine** — submit jobs and storage writes from the browser.
- **Real hardware or virtual boards** — with `ESPLAB_SERIAL=/dev/ttyUSB0`
  it talks to a real coordinator's USB serial console; without it, it
  spawns a virtual board and joins a local test cluster.
- **No dependencies** — a single Python file, standard library only.

## Install

```bash
git clone https://github.com/ESPlab-labs/ESPlab
cd ESPlab
python3 tools/webui/webui.py          # dashboard on http://localhost:8080
```

Against a real cluster (boards flashed per the
[hardware guide](https://github.com/ESPlab-labs/ESPlab/blob/main/docs/HARDWARE.md),
pyserial required):

```bash
ESPLAB_SERIAL=/dev/ttyUSB0 python3 tools/webui/webui.py
```

A standalone copy of this service also ships in this repo's
[Releases](https://github.com/ESPlab-labs/ESPlab-WebUI/releases) for use
without the full ESPlab checkout.

## Notes

The dashboard speaks the same serial console a person would type into — it
has no privileged path to the boards and can't do anything the console
can't. On the dashboard's startup it asks the cluster to re-run its
election so the strongest board coordinates; this keeps job status visible
to the dashboard (and to ESP On Demand) regardless of join order.

## License

[MIT](LICENSE)
