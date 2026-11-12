# TDA / Task Acceptance Exercise

Runs acceptance tests for three configured tasks, starts accepted tasks, and
cycles task information on an SSD1306 display. Review `boards/` and `prj.conf`
for the board and display configuration used by this project.

## Build

```bash
west build -p always -b esp32_devkitc/esp32/procpu --sysbuild path/to/Zephyr-practical/apps/tda
west flash
west espressif monitor
```
