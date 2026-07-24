# ADE9000 STM32H7 Driver

A lightweight C driver for the **Analog Devices ADE9000** three-phase energy metering IC targeting the **STM32H7** family using the **STM32Cube HAL** framework.

The driver is based on the **Analog Devices no-OS ADE9000 driver** and has been adapted for STM32Cube HAL. It provides a simple API for configuring the ADE9000 and accessing measurement registers over SPI.

The driver has been **developed and tested on the STM32 NUCLEO-H755ZI-Q** development board with the **STM32H755ZI** dual-core microcontroller. Although it was validated on this platform, it should be portable to other STM32H7 devices with minimal changes.

---

## Features

- STM32 HAL compatible
- SPI register read/write
- Read/modify/write register operations
- Device initialization and setup
- Temperature sensor support
- Voltage and current RMS measurements
- Burst waveform buffer read
- DMA waveform buffer acquisition
- DMA phase measurement block acquisition
- Utility functions for parsing burst data
- Energy accumulation configuration

---

## Repository Structure

```
ade9000-driver/
├── ade9000.c
├── ade9000.h
├── no_os_alloc.c
├── no_os_alloc.h
├── no_os_util.c
└── no_os_util.h
```

---

## Requirements

- STM32Cube HAL
- SPI peripheral configured
- GPIO output for Chip Select
- C99 compatible compiler

---

## Initialization

```c
struct ade9000_dev *ade;

struct ade9000_init_param init = {
    .hspi    = &hspi1,
    .cs_port = GPIOA,
    .cs_pin  = GPIO_PIN_4,
    .temp_en = true
};

ade9000_init(&ade, init);
ade9000_setup(ade);
```

---

## Basic Register Access

### Read Register

```c
uint32_t value;

ade9000_read(ade,
             ADE9000_REG_AVRMS,
             &value);
```

### Write Register

```c
ade9000_write(ade,
              ADE9000_REG_RUN,
              ADE9000_RUN_ON);
```

---

## Reading RMS Measurements

```c
ade9000_read_data_ph(ade, ADE9000_PHASE_A);

printf("Voltage : %lu mV\n", ade->vrms_val);
printf("Current : %lu mA\n", ade->irms_val);
```

---

## Waveform Buffer

The driver supports reading the ADE9000 waveform buffer using either blocking SPI or DMA.

### Blocking

```c
ade9000_wfb_burst_read(...);
```

### DMA

```c
ade9000_wfb_burst_read_DMA(...);
```

---

## Phase Measurement Block

The driver supports DMA acquisition of the ADE9000 phase measurement register block.

```c
ade9000_phase_block_read_DMA(...);

ade9000_parse_burst_block(...);
```

---

## Current Status

Implemented

- Register read/write
- Device initialization
- Device setup
- RMS measurements
- Temperature measurements
- Waveform buffer DMA
- Phase block DMA
- Energy accumulation configuration

Planned

- Calibration helper functions
- Harmonic measurement helpers
- Power and energy helper APIs
- Automatic conversion utilities

---

## License

This driver is derived from the **Analog Devices no-OS ADE9000 driver**. For the original implementation and documentation, see the [ADE9000 no-OS Doxygen Documentation](https://analogdevicesinc.github.io/no-OS/doxygen/ade9000_8c.html).

Additional STM32 HAL adaptations and extensions are released under the same BSD-style license.