# Zephyr Practical

A collection of Zephyr RTOS exercises and applications focused on real-time task
scheduling, synchronization, resource sharing, and embedded-system bring-up.

This repository is organised as independent Zephyr applications. Each application
has its own `CMakeLists.txt`, `prj.conf`, board configuration (where applicable),
and `src/` directory.

## Repository structure

```text
.
├── README.md
├── apps/
│   ├── chatterbox/       # Minimal periodic timer / time-printing example
│   ├── edf/              # Earliest Deadline First scheduling exercise
│   ├── pcp/              # Priority Ceiling Protocol and critical sections
│   └── tda/              # Task-deadline/acceptance-test exercise with display output
└── samples/
    └── hello_world/      # Minimal Zephyr Hello World sample
```

## Applications

| Directory | Purpose | Main implementation |
|---|---|---|
| `apps/edf` | Periodic task setup, acceptance testing, and a deferrable server | `src/main.c`, `src/tasks.c` |
| `apps/pcp` | Periodic tasks sharing resources, critical sections, and priority-ceiling handling | `src/main.c`, `src/tasks.c`, `src/critical_section.c` |
| `apps/tda` | Task acceptance testing and task information displayed on an SSD1306 display | `src/main.c`, `src/acceptance_test.c`, `src/display.c` |
| `apps/chatterbox` | Starts a Zephyr timer that prints elapsed time every second | `src/main.c` |
| `samples/hello_world` | Basic board-target Hello World output | `src/main.c` |

The EDF, PCP, and TDA applications include task-specific configuration and ESP32
board overlay files. `chatterbox` uses an ESP-WROVER-KIT overlay. Check each
application's `boards/` directory and `prj.conf` before changing the target board.

## Requirements

- A working Zephyr development environment.
- The Zephyr `west` tool and the SDK/toolchain required by your Zephyr installation.
- The board target and any hardware peripherals required by the selected exercise.
- For the display-based TDA exercise, the compatible SSD1306 display hardware.

These projects were provided as source files; the commands below are usage
templates and have not been validated against your local Zephyr workspace.

## Build and flash

Run commands from the root of your Zephyr workspace (the directory containing
`west.yml`), not necessarily from this repository's root. Adjust the relative
path to this repository if it is stored elsewhere.

### EDF

```bash
west build -p always -b esp32_devkitc/esp32/procpu --sysbuild path/to/Zephyr-practical/apps/edf
west flash
west espressif monitor
```

### PCP

```bash
west build -p always -b esp32_devkitc/esp32/procpu --sysbuild path/to/Zephyr-practical/apps/pcp
west flash
west espressif monitor
```

### TDA

```bash
west build -p always -b esp32_devkitc/esp32/procpu --sysbuild path/to/Zephyr-practical/apps/tda
west flash
west espressif monitor
```

### Chatterbox

```bash
west build -p always -b esp_wrover_kit/esp32/procpu --sysbuild path/to/Zephyr-practical/apps/chatterbox
west flash
west espressif monitor
```

### Hello World

```bash
west build -p always -b <your-board-target> path/to/Zephyr-practical/samples/hello_world
west flash
```

Replace `path/to/Zephyr-practical` with the actual path. For a build that does
not require sysbuild, remove `--sysbuild` if your Zephyr version/application
configuration does not use it. Use the board target supported by your installed
Zephyr version.

## Notes on the PCP exercise

The existing PCP exercise notes report two issues in the unmodified task/resource
scenario:

1. **Unbounded priority inversion:** a higher-priority task waiting for a resource
   can be delayed when a medium-priority task preempts the lower-priority task
   holding that resource.
2. **Deadlock:** tasks can acquire resources in conflicting orders and then wait
   indefinitely for resources held by one another.

Treat these as the observations recorded in the exercise notes; verify behaviour
with the assignment specification and your own run.

## Source layout conventions

- `src/` — application C source and headers.
- `boards/` — board-specific devicetree overlays.
- `prj.conf` — Zephyr Kconfig options for the application.
- `Kconfig` — application-specific configuration options.
- `CMakeLists.txt` — Zephyr build definition.
- `*.ld` — linker section fragments used by selected exercises.


