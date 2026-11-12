# Chatterbox

A minimal Zephyr timer example. A kernel timer invokes a callback every second
and prints an incrementing elapsed-time counter.

## Build

```bash
west build -p always -b esp_wrover_kit/esp32/procpu --sysbuild path/to/Zephyr-practical/apps/chatterbox
west flash
west espressif monitor
```
