# Priority Ceiling Protocol (PCP) Exercise

Demonstrates periodic tasks, shared resources, critical sections, and priority
ceiling initialization. The source configures three tasks and resources, performs
task acceptance checks, initializes priority ceilings, and starts accepted tasks.

## Recorded observation

The original exercise notes describe unbounded priority inversion and deadlock
in the unmodified resource-access scenario. See the root README for a short
explanation; confirm the behaviour against the assignment and a board run.

## Build

```bash
west build -p always -b esp32_devkitc/esp32/procpu --sysbuild path/to/Zephyr-practical/apps/pcp
west flash
west espressif monitor
```
