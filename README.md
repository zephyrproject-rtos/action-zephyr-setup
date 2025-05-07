# action-setup-zephyr

This action initializes a Zephyr based project, downloading the Zephyr SDK and
the necessary modules for a West based [Zephyr workspace application][1].

## Basic usage

```yaml
- name: Setup Zephyr project
  uses: zephyrproject-rtos/action-zephyr-setup@v1
  with:
    app-path: example-application
    toolchains: arm-zephyr-eabi
```

## Scenarios

### Application and west.yml in an "app" subdirectory

```yaml
- name: Checkout
  uses: actions/checkout@v3

- name: Setup Zephyr project
  uses: zephyrproject-rtos/action-zephyr-setup@v1
  with:
    app-path: app
    toolchains: arm-zephyr-eabi

- name: Build
  run: |
    west build app
```

### Application and west.yml at the root of the repository

```yaml
- name: Checkout
  uses: actions/checkout@v3
  with:
    path: app

- name: Setup Zephyr project
  uses: zephyrproject-rtos/action-zephyr-setup@v1
  with:
    app-path: app
    toolchains: arm-zephyr-eabi

- name: Build
  run: |
    west build app
```

### Use a specific SDK version and multiple compilers

```yaml
- name: Setup Zephyr project
  uses: zephyrproject-rtos/action-zephyr-setup@v1
  with:
    app-path: app
    toolchains: arm-zephyr-eabi:riscv64-zephyr-elf
    sdk-version: 0.16.3
```

## Specify a custom west workspace manifest file name

```yaml
- name: Setup Zephyr project
  uses: zephyrproject-rtos/zephyr-setup@v1
  with:
    app-path: app
    toolchains: arm-zephyr-eabi
    manifest-file-name: custom_west.yml
```

## Filter west groups and projects

```yaml
- name: Setup Zephyr project
  uses: zephyrproject-rtos/zephyr-setup@v1
  with:
    app-path: app
    toolchains: arm-zephyr-eabi
    west-group-filter: -hal,-tools,-bootloader,-babblesim
    west-project-filter: -nrf_hw_models
```

## Skip installing OS level dependencies and Zephyr SDK

```yaml
- name: Setup Zephyr project
  uses: zephyrproject-rtos/action-zephyr-setup@v1
  with:
    app-path: example-application
    toolchains: arm-zephyr-eabi
    skip-dependencies: true
```

[1]: https://docs.zephyrproject.org/latest/develop/application/index.html#zephyr-workspace-app
