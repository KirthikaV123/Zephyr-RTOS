# EDF Scheduling Exercise

Implements periodic task setup, task acceptance checks, and a deferrable server.
The entry point registers task definitions and creates threads for tasks that
pass the acceptance test (the deferrable server is created separately).

## Build

From your Zephyr workspace root:

```bash
west build -p always -b esp32_devkitc/esp32/procpu --sysbuild path/to/Zephyr-practical/apps/edf
west flash
west espressif monitor
```

See the repository-level README for environment requirements and path notes.
