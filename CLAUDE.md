# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

This is a ZMK firmware configuration for a custom 2x5 macropad. ZMK is a modern keyboard firmware built on the Zephyr RTOS that supports wireless connectivity and advanced features.

## Build Process

The project uses GitHub Actions for automated builds. The build configuration is defined in `build.yaml` which specifies:
- Board: `nice_nano_v2` 
- Shield: `2x5macropad`

Local builds are not typically needed as firmware is built automatically via GitHub Actions when changes are pushed.

## Architecture

### Key Components

- **West Configuration** (`config/west.yml`): Defines the ZMK firmware dependency and project structure
- **Build Configuration** (`build.yaml`): Specifies board/shield combinations for CI builds
- **Shield Definition** (`config/boards/shields/2x5macropad/`):
  - `Kconfig.shield`: Shield identifier configuration
  - `Kconfig.defconfig`: Default keyboard name configuration
  - `macropad.overlay`: Hardware definition (GPIO pins, matrix configuration)
  - `macropad.keymap`: Key mappings and behavior definitions

### Hardware Layout

The macropad uses a 2x5 matrix (2 rows, 5 columns) with GPIO matrix scanning:
- Row pins: GPIO 5-9 on the pro-micro
- Column pins: GPIO 10, 16 on the pro-micro  
- Diode direction: col2row

### File Structure

- `config/`: Main configuration directory containing west.yml and shield definitions
- `boards/shields/`: Empty directory (shields are defined in config/boards/shields/)
- `zephyr/module.yml`: Zephyr module configuration with board_root setting
- `.github/workflows/build.yml`: CI/CD pipeline using ZMK's build workflow

## Development Workflow

1. Modify keymap or shield configuration files
2. Commit and push changes
3. GitHub Actions automatically builds firmware
4. Download firmware artifacts from Actions tab
5. Flash to the nice_nano_v2 controller

The project follows ZMK's standard configuration structure and leverages the upstream build system for all compilation tasks.