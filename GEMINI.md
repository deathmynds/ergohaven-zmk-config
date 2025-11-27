# Ergohaven ZMK Config

This repository contains ZMK firmware configurations for various Ergohaven custom keyboards, including `velvet_v3`, `op36`, `k03`, `imperial44`, and `trackball`. It leverages the ZMK framework to define keymaps, behaviors, and board-specific settings.

## Project Overview

The project's primary purpose is to manage and build custom firmware for Ergohaven keyboards using the ZMK firmware. It provides specific keymap layouts (e.g., `_ruen` for Russian-English layouts), board configurations, and build definitions for different shield combinations (e.g., `_qube`, `_ui`). The `build.yaml` file orchestrates the generation of various firmware artifacts.

## Building and Running

The project utilizes `west` (Zephyr's meta-tool) for managing dependencies and building the ZMK firmware. The actual build process is handled by a reusable GitHub Actions workflow (`.github/workflows/build.yml`) provided by `ergohaven/ergohaven-zmk`.

To build a specific keymap locally, you would typically use the `west build` command. Based on the `build.yaml`, an example command for building the `imperial44_ruen` keymap for the `imperial44_left` shield would be:

```bash
west build -s zmk/app -b ergohaven -- -DSHIELD=imperial44_left -DKEYMAP=imperial44_ruen
```

To build a version for a QUBE shield (wireless), for example, `imperial44_qube_ruen`:

```bash
west build -s zmk/app -b ergohaven -- -DSHIELD=imperial44_qube -DKEYMAP=imperial44_ruen
```

The `build.yaml` file contains a comprehensive list of all supported build configurations and their corresponding artifact names.

## Development Conventions

*   **Keymap Files:** Located in the `config/` directory, following the naming convention `[keyboard_name].keymap` or `[keyboard_name]_[language_code].keymap`. These files define the key assignments for different layers.
*   **Configuration Files:** Also in `config/`, e.g., `[keyboard_name].conf`. These files contain ZMK-specific configuration options (e.g., sleep settings, battery reporting).
*   **Layout JSON Files:** Found in `config/`, e.g., `[keyboard_name].json`. These files define the physical key layout and coordinates, primarily used for visualization tools like ZMK Studio.
*   **West Manifest:** `config/west.yml` specifies external ZMK modules and dependencies, particularly the `ergohaven-zmk` repository itself.
*   **Build Definitions:** `build.yaml` defines the various build targets, including specific board, shield, and keymap combinations, along with custom CMake arguments and artifact names.
